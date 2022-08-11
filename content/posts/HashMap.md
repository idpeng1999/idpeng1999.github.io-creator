---
title: "HashMap"
date: 2022-03-17T13:14:21+08:00
draft: false
categories: [java知识]
---


相比于JDK7，HashMap在JDK8中做链表结构做了优化（但仍然线程不安全），在一定条件下将链表转为红黑树，提升查询效率。

## put()操作

* 先根据key确定在哈希table中的下标，找到对应的bucket，遍历链表（或红黑树），做插入操作。 
* 在JDK7中，新增结点是使用头插法，但在JDK8中，在链表使用尾插法，将待新增结点追加到链表末尾。

![Put](/img/HashMap/1.png)

红黑树的转换操作如下：

```java
/**
 * Replaces all linked nodes in bin at index for given hash unless
 * table is too small, in which case resizes instead.
 */
final void treeifyBin(Node<K,V>[] tab, int hash) {
    int n, index; Node<K,V> e;
    // 若表为空，或表长度小于MIN_TREEIFY_CAPACITY，也不做转换，直接做扩容处理。
    if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
        resize();
    else if ((e = tab[index = (n - 1) & hash]) != null) {
        TreeNode<K,V> hd = null, tl = null;
        do {
            TreeNode<K,V> p = replacementTreeNode(e, null);
            if (tl == null)
                hd = p;
            else {
                p.prev = tl;
                tl.next = p;
            }
            tl = p;
        } while ((e = e.next) != null);
        if ((tab[index] = hd) != null)
            hd.treeify(tab);
    }
}
```

## 扩容操作

什么场景下会触发扩容？

* 哈希table为null或长度为0； 
* Map中存储的k-v对数量超过了阈值threshold； 
* 链表中的长度超过了TREEIFY_THRESHOLD，但表长度却小于MIN_TREEIFY_CAPACITY。

一般的扩容分为2步，第1步是对哈希表长度的扩展（2倍），第2步是将旧table中的数据搬到新table上。

那么，在JDK8中，HashMap是如何扩容的呢？

```java
// 前面已经做了第1步的长度拓展，我们主要分析第2步的操作：如何迁移数据
table = newTab;
if (oldTab != null) {
    // 循环遍历哈希table的每个不为null的bucket
    // 注意，这里是"++j"，略过了oldTab[0]的处理
    for (int j = 0; j < oldCap; ++j) {
        Node<K,V> e;
        if ((e = oldTab[j]) != null) {
            oldTab[j] = null;
            // 若只有一个结点，则原地存储
            if (e.next == null)
                newTab[e.hash & (newCap - 1)] = e;
            else if (e instanceof TreeNode)
                ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
            else { // preserve order
                // "lo"前缀的代表要在原bucket上存储，"hi"前缀的代表要在新的bucket上存储
                // loHead代表是链表的头结点，loTail代表链表的尾结点
                Node<K,V> loHead = null, loTail = null;
                Node<K,V> hiHead = null, hiTail = null;
                Node<K,V> next;
                do {
                    next = e.next;
                    // 以oldCap=8为例，
                    //   0001 1000  e.hash=24
                    // & 0000 1000  oldCap=8
                    // = 0000 1000  --> 不为0，需要迁移
                    // 这种规律可发现，[oldCap, (2*oldCap-1)]之间的数据，
                    // 以及在此基础上加n*2*oldCap的数据，都需要做迁移，剩余的则不用迁移
                    if ((e.hash & oldCap) == 0) {
                        // 这种是有序插入，即依次将原链表的结点追加到当前链表的末尾
                        if (loTail == null)
                            loHead = e;
                        else
                            loTail.next = e;
                        loTail = e;
                    }
                    else {
                        if (hiTail == null)
                            hiHead = e;
                        else
                            hiTail.next = e;
                        hiTail = e;
                    }
                } while ((e = next) != null);
                if (loTail != null) {
                    loTail.next = null;
                    newTab[j] = loHead;
                }
                if (hiTail != null) {
                    hiTail.next = null;
                    // 需要搬迁的结点，新下标为从当前下标往前挪oldCap个距离。
                    newTab[j + oldCap] = hiHead;
                }
            }
        }
    }
}
```

## get()操作

* 先根据key计算hash值，进一步计算得到哈希table的目标index
* 若此bucket上为红黑树，则再红黑树上查找，若不是红黑树，遍历链表。

```java
public V get(Object key) {
    Node<K,V> e;
    return (e = getNode(hash(key), key)) == null ? null : e.value;
}


final Node<K,V> getNode(int hash, Object key) {
    Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
    if ((tab = table) != null && (n = tab.length) > 0 &&
        (first = tab[(n - 1) & hash]) != null) {
        if (first.hash == hash && // always check first node
            ((k = first.key) == key || (key != null && key.equals(k))))
            return first;
        if ((e = first.next) != null) {
            if (first instanceof TreeNode)
                return ((TreeNode<K,V>)first).getTreeNode(hash, key);
            do {
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    return e;
            } while ((e = e.next) != null);
        }
    }
    return null;
}
```

## HashMap、HashTable是什么关系？

共同点:

* 底层都是使用哈希表 + 链表的实现方式。

异同点:

* 从层级结构上看，HashMap、HashTable有一个共用的Map接口。另外，HashTable还单独继承了一个抽象类Dictionary；
* HashTable线程安全，HashMap线程不安全；
* 初始值和扩容方式不同。HashTable的初始值为11，扩容为原大小的`2*d+1`。
容量大小都采用奇数且为素数，且采用取模法，这种方式散列更均匀。
但有个缺点就是对素数取模的性能较低（涉及到除法运算）,
而HashTable的长度都是2的次幂，设计就较为巧妙，这种方式的取模都是直接做位运算，性能较好。
* HashMap的key、value都可为null，且value可多次为null，key多次为null时会覆盖。
当HashTable的key、value都不可为null，否则直接NPE(NullPointException)。

## 保证HashMap的线程安全

* 可以添加synchronized关键字





