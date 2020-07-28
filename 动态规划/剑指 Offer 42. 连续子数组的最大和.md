#### [剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

##### 方法一：暴力 时间复杂度（n*n)

​	略

##### 方法二：动态规划

首先需要确定的是找出状态转移方程

```
	   dp[i-1]+num[i]   d[i-1]>0
dp[i]=	
		num[i]          d[i-1]<=0    

```



```
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

d[i] 为第位置的和，这个和并不是从0开始的和

如果d[i-1]的和是负数，那么相当于前面的和是累赘，因为负数+一个数<这个数。

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        // 不能为0，至少要选一个
        int len=nums.size();
        if(len==0) return 0;
        vector<int>d(len+1);
        d[0]=-INT_MAX;
        int res=d[0];
        for(int i=0;i<len;i++){  
            if(d[i]<=0)
                d[i+1]=nums[i];
            else 
                d[i+1]=d[i]+nums[i];
            res =max(res,d[i+1]);
        }  
        return res;
    }
};
```

其实没必要n的空间复杂度

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        // 不能为0，至少要选一个
        int len=nums.size();
        if(len==0) return 0;
        int local=-INT_MAX;
        int res=local;
        for(int i=0;i<len;i++){  
           local= local<=0?nums[i]:local+nums[i];
            res =max(res,local);
        }  
        return res;
    }
};
```

##### 方法三：分治算法

分治法模板： 

1. 定义基本情况 
2. 将问题分解为子问题并递归解决子问题 
3. 合并子问题的解以获得原始问题的解 

三种情况

将nums在中点mid分成三种

​	1：最长数列在mid左边

​	2：最长数列在mid右边

​	3：最大子串跨中点，左右都有

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if(nums.size()==0) return 0;
      return  divide(nums,0,nums.size()-1);
    }
    int divide(vector<int>&nums,int left,int right){
        if(left==right) return nums[left];
        int mid=(left+right)/2;
        // 1:最大数列和在左边
        int sumleft=divide(nums,left,mid);
        // 2.最大数列和在右边
        int sumright =divide(nums,mid+1,right);
        // 3.最大数列和在中间
        // 先求左边最大和
        int leftsum=0,leftMaxsum=INT_MIN;
        for(int i=mid;i>=left;i--){
            leftsum+=nums[i];
            leftMaxsum=max(leftMaxsum,leftsum);
        }
        // 先求右边最大和
        int rightsum=0,rightMaxsum=INT_MIN;
        for(int i=mid+1;i<=right;i++){
            rightsum+=nums[i];
            rightMaxsum=max(rightMaxsum,rightsum);
        }
        return max(max(sumleft,sumright),leftMaxsum+rightMaxsum);
    }
};
```

分治算法参考：
https://leetcode-cn.com/problems/contiguous-sequence-lcci/solution/fen-zhi-he-dong-tai-gui-hua-liang-chong-jie-fa-by-/

