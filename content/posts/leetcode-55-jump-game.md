---
title: "Leetcode 55 Jump Game"
date: 2018-10-15T08:02:25+08:00
draft: false
---

可以用动态规划的方法。

## DP, beats 5%

{{<highlight cpp>}}
class Solution {
public:
   bool canJump(vector<int> &nums) {
     std::vector<bool> jumpable(nums.size(), false);
     jumpable.front() = true;
    for (int i = 0; i < nums.size(); i++) {
      if (!jumpable[i])
        continue;
      for (int j = 1; j <= nums[i]; j++) {
        if (i + j < nums.size())
          jumpable[i + j] = true;
      }
    }
    return jumpable.back();
  }
};
{{</highlight>}}


## DP 优化版, beats 95%

{{<highlight cpp>}}
class Solution {
public:
  bool canJump(vector<int> &nums) {
    if (nums.empty() || nums.size() == 1)
      return true;

    bool non_zero = true;
    for (auto v : nums) {
      // cout << v << endl;
      if (v == 0) {
        non_zero = false;
        break;
      }
    }
    // cout << "non_zero " << non_zero << endl;
    if (non_zero)
      return true;

    int sum = 0;
    int i = 0;
    for (auto v : nums) {
      if (++i == nums.size())
        return true;
      sum--;
      sum = max(sum, v);
      // cout << "sum " << sum << endl;
      if (sum == 0)
        return false;
    }
    return true;
  }
};

{{ </highlight> }}

