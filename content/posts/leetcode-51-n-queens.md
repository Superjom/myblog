---
title: "Leetcode 51 N Queens"
date: 2018-10-17T07:59:30+08:00
draft: true
---

# 递归方法 12ms, beats 19%

{{<highlight cpp>}}

class Solution {
 public:
  vector<vector<string>> solveNQueens(int n) {
    this->n = n;
    PlaceRecur(0);
    return result;
  }

  void PlaceRecur(int y) {
    if (y >= n) return;
    std::pair<int, int> pos;
    pos.second = y;

    for (int x = 0; x < n; x++) {
      pos.first = x;
      if (tryPlace(pos)) {
        PlaceRecur(y + 1);
        RemovePlace(pos);
      }
    }
  }

  inline bool tryPlace(std::pair<int, int> &pos) {
    int x = getX(pos);
    int y = getY(pos);
    if (x >= n || y >= n) return false;
    int bevel0 = getBevel0(pos);
    int bevel1 = getBevel1(pos);

    if (xs.count(x) || ys.count(y) || bevel0s.count(bevel0) || bevel1s.count(bevel1)) return false;
    xs.insert(x);
    ys.insert(y);
    bevel0s.insert(bevel0);
    bevel1s.insert(bevel1);
    poses.push_back(pos);

    if (y == n - 1) {
      // collect result
      std::vector<std::string> res(n, std::string(n, '.'));

      for (auto &pos : poses) {
        res[getY(pos)][getX(pos)] = 'Q';
      }
      result.emplace_back(res);
    }
    return true;
  }

  inline void RemovePlace(std::pair<int, int> &pos) {
    int x = getX(pos);
    int y = getY(pos);
    int bevel0 = getBevel0(pos);
    int bevel1 = getBevel1(pos);
    xs.erase(x);
    ys.erase(y);
    bevel0s.erase(bevel0);
    bevel1s.erase(bevel1);
    poses.pop_back();
  }

  inline int getX(std::pair<int, int> &pos) {
    return pos.first;
  }
  inline int getY(std::pair<int, int> &pos) {
    return pos.second;
  }
  inline int getBevel0(std::pair<int, int> &pos) {
    int x = getX(pos);
    int y = getY(pos);
    return y - x;
  }
  inline int getBevel1(std::pair<int, int> &pos) {
    int x = getX(pos);
    int y = getY(pos);
    return y + x;
  }

  std::unordered_set<int> xs;
  std::unordered_set<int> ys;
  std::unordered_set<int> bevel0s;
  std::unordered_set<int> bevel1s;
  std::vector<std::pair<int, int>> poses;
  int n{0};
  std::vector<std::vector<string>> result;
  };

{{</highlight>}}
