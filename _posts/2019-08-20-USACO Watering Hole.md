---
layout: post
title: "USACO Watering Hole"
date: 2019-08-20
excerpt: "Kruskal"
tags: [USACO]
comments: true
---
### ~~机房模拟赛10分的窝~~

### 当时想到了MST但是没有考虑太多

### ~~拿了十分~~

## 认真思考的话就发现了一个隐藏的条件就是打水的井

## 可以单独作为一个点连起来

```cpp
for (int i = 1;i <= n;++i){
	cin >> w[i];
	add_edge(i,0,w[i]);
	add_edge(0,i,w[i]);
}
```

## MST的话我还是选择Kruskal叭(毕竟不会写Prim)

### %%%题解区写Prim的巨佬们

## 上代码

```cpp
#include <iostream>
#include <cstdio>
#include <iomanip>
#include <cstring>
#include <vector>
#include <queue>
#include <cmath>
#include <algorithm>

using namespace std;
const int maxn = 310000;
struct node{
	int u,v,c,nxt;
}e[maxn];
int n,ans,a,w[maxn],head[maxn],cnt = 0;
int fa[maxn];
inline void add_edge(int u,int v,int c){
	e[++cnt].u = u;
	e[cnt].v = v;
	e[cnt].c = c;
	e[cnt].nxt = head[u];
	head[u] = cnt;
}
inline int find(int u){
	if (fa[u] == u)return u;
	else return fa[u] = find(fa[u]);
}
void Kruskal(){
	for (int i = 0;i <= cnt;++i){
		int fax = find (e[i].u),fay = find (e[i].v);
		if (fax == fay)continue;
		fa[fax] =fay;
		ans += e[i].c;
	}
}
bool cmp (node a,node b){
	return a.c < b.c;
}
int main(){
	cin >> n;
	for (int i = 1;i <= n;++i){
	cin >> w[i];
	add_edge(i,0,w[i]);
	add_edge(0,i,w[i]);
	}
	for (int i = 1;i <= n;++i)
		for (int j = 1;j <= n;++j){
			cin >> a;
			if (i > j)
				add_edge(i,j,a);
		}
	for (int i = 1;i <= n;++i)fa[i] = i;
	sort (e,e+cnt+1,cmp);
	Kruskal();
	cout << ans;
	return 0;
}
```
