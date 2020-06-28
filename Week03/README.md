

# 作业题 

## 1.[二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/) 
**递归--二叉树的后序遍历方式**
时间复杂度O(n) ==》 遍历所有节点
空间复杂度O(logn) 取决于二叉树的深度,最坏情况二叉树退化为链表

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        //terminator
        if (root == null || root == p || root == q) return root;
        //drill down 
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        //process (后序遍历)
        return left == null ? right : right == null ? left : root;
    }
}
```

思考：当遇到二叉树的题目时 由于二叉树本身定义就是一种递归定义 所以重复子问题 似乎显而易见。但有些题目会很难找到最近重复子问题，需要有对问题的建模能力，找到简单的子问题，并且设计要传递到下一层的共享变量，但好消息是递归本身是一层一层下探，然后对称性地一层层向上返回，基本不会跳层，但可以自定义逻辑进行减枝来提高性能，以及缓存一些重复性的子问题求解来优化。

递归难点：在于抽象出重复子问题并设计好主角；



## 2.[组合](https://leetcode-cn.com/problems/combinations/) 

**回溯方式 + 优化剪枝**

```
时间复杂度 : O(k C_N^k)，其中 C_N^k = \frac{N!}{(N - k)! k!}是要构成的组合数
空间复杂度 : O(C_N^k) ，用于保存全部组合数以输出.
```

```
class Solution {

    List<List<Integer>> result = new LinkedList();
    int n;
    int k;

  public void backtrack(int first, LinkedList<Integer> curr) {
    // if the combination is done
    if (curr.size() == k) {
        result.add(new LinkedList(curr));
        return ;
    }
    for (int i = first; i < n + 1; ++i) {
      // add i into the current combination
      curr.add(i);
      // use next integers to complete the combination
      backtrack(i + 1, curr);
      // backtrack ==> reverse current states
      curr.removeLast();
    }
  }

  public List<List<Integer>> combine(int n, int k) {
    this.n = n;
    this.k = k;
    backtrack(1, new LinkedList<Integer>());
    return output;
  }

}


```

