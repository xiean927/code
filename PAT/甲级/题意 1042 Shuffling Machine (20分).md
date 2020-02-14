* 题意理解
* If the number at the i-th position is j, it means to move the card from position i to position j. 
  * For example, suppose we only have 5 cards: S3, H5, C1, D13 and J2. 
  * Given a shuffling order {4, 2, 5, 3, 1}, the result will be: J2, H5, D13, S3, C1. 
  * If we are to repeat the shuffling again, the result will be: C1, H5, S3, J2, D13.

* 样例解析
```
2
36 52 37 38 3 39 40 53 54 41 11 12 13 42 43 44 2 4 23 24 25 26 27 6 7 8 48 49 50 51 9 10 14 15 16 5 17 18 19 1 20 21 22 28 29 30 31 32 33 34 35 45 46 47

第一次洗牌
0号到位置36
1号到位置52

```
