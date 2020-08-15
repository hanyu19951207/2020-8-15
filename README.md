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
