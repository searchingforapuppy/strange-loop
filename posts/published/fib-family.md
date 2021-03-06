---
title: "フィボナッチ・ファミリー"
created: "2021-09-10"
updated: "2021-09-10"
---

OEIS から適当な数列を眺めていると、フィボナッチ数列と似たタイプの数列がかなりあることに気づく。ここでは、ぼくが見つけた物の中で、それらをざっと並べてみようと思う。
これは、新たなものをぼくが見つけ次第適宜追加していく。

## フィボナッチ・ファミリーの定義

- 整数列である
- 数列の最初の数項は定数として与えられる
- 以降の数列の要素は漸化式で表現される

## フィボナッチ・ファミリー

| 番号(OEIS) | 一般名称             | 定数項         | 漸化式                    |
| :--------- | :------------------- | :------------- | :------------------------ |
| A000045    | フィボナッチ数列　   | F(0)=0, F(1)=1 | F(n)=F(n-1)+F(n-2)        |
| A000129    | ペル数列             | F(0)=0, F(1)=1 | F(n)=2F(n-1)+F(n-2)       |
| A000058    | Sylvester's sequence | F(0)=2         | F(n+1)= F(n)^2 - F(n) + 1 |
