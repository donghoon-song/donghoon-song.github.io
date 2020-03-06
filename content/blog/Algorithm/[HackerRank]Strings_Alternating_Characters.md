---
title: '[HackerRank]Strings: Alternating Characters'
date: 2020-02-19 21:17:00
category: Algorithm
draft: false
---

[문제](https://www.hackerrank.com/challenges/alternating-characters/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings)

```cpp{3}
function alternatingCharacters(s) {
    let ans = 0;
    for(let i=0; i<s.length-1; i++) {
        if(s[i]==s[i+1])
            ans++;
    }
    return ans;
}
```
