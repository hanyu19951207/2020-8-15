# 2020-8-15
532. 数组中的K-diff数对
    给定一个整数数组和一个整数 k, 你需要在数组里找到不同的 k-diff 数对。这里将 k-diff 数对定义为一个整数对 (i, j), 其中 i 和 j 都是数组中的数字，且两数之差的绝对值是 k.
    示例 1:
    输入: [3, 1, 4, 1, 5], k = 2
    输出: 2
    解释: 数组中有两个 2-diff 数对, (1, 3) 和 (3, 5)。
    尽管数组中有两个1，但我们只应返回不同的数对的数量。
思路：
    先给数组排序，然后利用有序性，加一条if(i >= 1 && nums[i] == nums[i -1]) continue;语句来排序重复元素
    然后利用双重循环遍历数组。
题解:
class Solution {
    public int findPairs(int[] nums, int k) {
        if(nums.length < 2)
            return 0;
        Arrays.sort(nums);
        int count = 0;
        for(int i = 0;i < nums.length - 1;i++){
            if(i >= 1 && nums[i] == nums[i - 1])
                continue;
            for(int j = i + 1;j < nums.length;j++){
                if(nums[j] - nums[i] != k)
                    continue;
                if(nums[j] - nums[i] == k){
                    count++;
                    break;
                }
            }
        }
        return count;
    }
}
538. 把二叉搜索树转换为累加树
    给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)，使得每个节点的值是原来的节点值加上所有大于它的节点值之和。
    例如：
    输入: 原始二叉搜索树:
                  5
                /   \
               2     13
    输出: 转换为累加树:
                 18
                /   \
              20     13
思路：
    在递归方法中，我们维护一些递归调用过程中可以访问和修改的全局变量。首先我们判断当前访问的节点是否存在，如果存在就递归右子树，递归回来的时候更新总和和当前点的值，然后递归左子树。
    如果我们分别正确地递归 root.right 和 root.left ，那么我们就能正确地用大于某个节点的值去更新此节点，然后才遍历比它小的值。
题解：
class Solution {
    private int sum = 0;
    public TreeNode convertBST(TreeNode root) {
        if(root != null){
            convertBST(root.right);
            sum += root.val;
            root.val = sum;
            convertBST(root.left);
        }
        return root;
    }
}
541. 反转字符串 II
    给定一个字符串 s 和一个整数 k，你需要对从字符串开头算起的每隔 2k 个字符的前 k 个字符进行反转。
    如果剩余字符少于 k 个，则将剩余字符全部反转。
    如果剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符，其余字符保持原样。
    示例:
    输入: s = "abcdefg", k = 2
    输出: "bacdfeg"
思路：
    我们直接翻转每个 2k 字符块。
    每个块开始于 2k 的倍数，也就是 0, 2k, 4k, 6k, ...。需要注意的一件是：如果没有足够的字符，我们并不需要翻转这个块。
    为了翻转从 i 到 j 的字符块，我们可以交换位于 i++ 和 j-- 的字符。
题解：
class Solution {
    public String reverseStr(String s, int k) {
        char [] ch = s.toCharArray();
        int n = ch.length;
        for(int i = 0;i < n;i += 2 * k){
            int left = i;
            int rigth = (i + k - 1 < n) ? i + k - 1 : n - 1;
            while(left <= rigth){
                char temp = ch[left];
                ch[left] = ch[rigth];
                ch[rigth] = temp;
                left++;
                rigth--;
            }
        }
        String str = new String(ch);
        return str;
    }
}
