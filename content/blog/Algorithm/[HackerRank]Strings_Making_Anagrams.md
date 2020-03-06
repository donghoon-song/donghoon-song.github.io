---
title: '[HackerRank]Strings: Making Anagrams'
date: 2020-02-19 08:57:00
category: Algorithm
draft: false
---

[문제](https://www.hackerrank.com/challenges/ctci-making-anagrams/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings)

```cpp{3}
int makeAnagram(string a, string b) {
    int nums1[26];
    int nums2[26];
    int ans = 0;
    for (int i = 0; i < 26; i++) {
        nums1[i] = 0;
        nums2[i] = 0;
    }
    for (int i = 0; i < a.size(); i++) {
        nums1[a[i] - 'a']++;
    }
    for (int i = 0; i < b.size(); i++) {
        nums2[b[i] - 'a']++;
    }
    for (int i = 0; i < 26; i++) {
        ans += nums1[i] - nums2[i] > 0 ? nums1[i] - nums2[i] : -(nums1[i] - nums2[i]);
    }
    return ans;

}
```
