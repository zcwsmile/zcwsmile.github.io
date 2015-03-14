---
layout: post
title: 除单词外反转字符串（反读）
category: 技术
tags:  reverse string
keywords:  reverse string
description:
---

```
#include <iostream>
using namespace std;

void RevStr(char sz[], int iLeft, int iRight)
{
	while (iLeft < iRight)
	{
		char cTmp = sz[iLeft];
		sz[iLeft] = sz[iRight];
		sz[iRight] = cTmp;

		iLeft++;
		iRight--;
	}
}

void RevStrButWord(char sz[])
{
	RevStr(sz, 0, strlen(sz)-1);

	unsigned int p1 = 0;
	unsigned int p2 = p1;
	while (p2 < strlen(sz))
	{
		while (sz[p1] == ' ' && sz[p1] != '\0') p1++;
		p2 = p1;
		while (sz[p2] != ' ' && sz[p2] != '\0') p2++;
		p2--;

		RevStr(sz, p1, p2);
		p1 = p2+2;
		p2 = p1;
	}
}

void main()
{
	char sz[] = "You  Love  China";
	RevStrButWord(sz);
	cout << sz <<endl;
}

//输出将是：“China  Love  You”。思想：先每个单词反转，然后全部反转就OK了。
```