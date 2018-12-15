---
title: "Leetcode 67 Add Binary"
date: 2018-10-27T13:51:04+08:00
draft: false
---

注意事项：

- ASCII 的处理
- for 循环中，避免太多的 if-else.

{{<highlight cpp>}}
class Solution {
public:
    string addBinary(string a, string b) {
        if (a.empty()) return b;
        if (b.empty()) return a;
        int mod = '0'+2;
        bool inc = false;
        
        string& llong = a.size() > b.size() ? a : b;
        string& sshort = a.size() <= b.size() ? a : b;
        
        //cout << "long " << llong << endl;
        //cout << "short " << sshort << endl;
        
        for (int i = 0; i < sshort.size(); i++) {
            char& ll = llong[llong.size() - 1 - i];
            ll += sshort[sshort.size() - 1 - i] + inc - '0';
            
            //cout << ll << endl;
            if (ll >= mod) {
                ll -= 2;
                inc = true;
            } else {
                inc = false;
            }
            
            llong[llong.size() - 1 - i] = ll;
        }
        
        for (int i = sshort.size(); i < llong.size(); i++) {
            if (!inc) break;
            
            char& ll = llong[llong.size() - 1 - i];
            ll += inc;
            
            if (ll >= mod) {
                ll -= 2;
                inc = true;
            } else {
                inc = false;
            }
            
            llong[llong.size() - 1 - i] = ll;
        }
        
        
        if (inc) {
            llong.insert(llong.begin(), '1');
        }
        
        return llong;
    }
};
{{ </highlight> }}
