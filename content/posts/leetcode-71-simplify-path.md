---
title: "Leetcode 71 Simplify Path"
date: 2018-10-31T09:50:43+08:00
draft: true
---



注意 `getline` 的简化

```c++
class Solution {
public:
    string simplifyPath(string path) {
        std::istringstream paths(path);
        std::string dir;
        std::deque<std::string> stack0;
        while(getline(paths, dir, '/')) {
            if (dir == ".") continue;
            else if (dir == "..") {
                if(!stack0.empty()) stack0.pop_back();
            } else if(!dir.empty()){
                stack0.push_back(dir);
            }
        }
        
        std::stringstream ss;
        ss << "/";
        while(stack0.size() > 1) {
            ss << stack0.front() << "/";
            stack0.pop_front();
        }
        if (!stack0.empty()) ss << stack0.back();
        
        return ss.str();
    }
};
```

