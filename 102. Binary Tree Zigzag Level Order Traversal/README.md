昨天刚总结完所有常见的二叉树遍历，今天就再遇一道。

此题是非常明显的层次遍历，显然应该想到 BFS，但略有不同的是，它要求曲折输出。啥意思？就是说偶数行，要逆向输出节点值。

这也很好理解，不会影响大体思路，需要考虑的就是，如何在 BFS 中知道进行到哪一层了。

对于这一点，我想了很多办法。递归、双栈、一栈一队列。结果本以为会很巧妙的解决，但总有几个 test case 让你绝望。

我无奈之下选择比较笨的一个办法，就是手动的记录 size， 最终也解决了这个问题。

----

思路是，在常规的 BFS 中准备三个标记：

```cpp
bool reverse = false; // 第一层不逆向
int cur_level_sz = 1, next_level_sz = 0; // 第一层，仅有一个根节点，故前者为 1，下一层需要在 BFS 中记录，故初始化为 0.
```

如何判断从上层下降到下层？

```cpp
if (cur_level_sz == 0) // 当前层的 size 递减到 0. 证明到了下一层
{
    retv.push_back(reverse ? vector<int>(v.crbegin(), v.crend()) : v); // 若需要逆向，则存储逆，否则直接存储 v
    v.clear(); // 每到下一层，都要清空
    cur_level_sz = next_level_sz; next_level_sz = 0; // 新的一层重新初始化
    reverse = !reverse; // 隔行逆向
}
```

没用递归，但效率仍一般，希望有高人指点我更高效的解法。
