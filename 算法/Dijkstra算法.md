### dijkstra最短路径算法

**a.**初始时，S只包含源点，即S＝{v}，v的距离为0。U包含除v外的其他顶点，即:U={其余顶点}，若v与U中顶点u有边，则<u,v>正常有权值，若u不是v的出边邻接点，则<u,v>权值为∞。

**b.**从U中选取一个距离v最小的顶点k，把k，加入S中（该选定的距离就是v到k的最短路径长度）。

**c.**以k为新考虑的中间点，修改U中各顶点的距离；若从源点v到顶点u的距离（经过顶点k）比原来距离（不经过顶点k）短，则修改顶点u的距离值，修改后的距离值的顶点k的距离加上边上的权。

**d.**重复步骤b和c直到所有顶点都包含在S中。



```c++
#include <iostream>

#include <vector>
#include <cmath>
#include <cstring>
#include <algorithm>
#include <map>
#include <queue>
#include <iomanip>
using namespace std;

struct node {
	int now, dist;
	bool operator<(const node &b) const {
		return this->dist > b.dist;
	}
};

int n, m, s, dis[1005][1005], ans[1005];

int main() {
	memset(dis, 0x3f, sizeof(dis));
	memset(ans, 0x3f, sizeof(ans));
	cin >> n >> m >> s;
	for (int i = 0; i < m; i++) {
		int a, b, c;
		dis[a][b] = min(dis[a][b], c);
	}
	priority_queue<node> que;
	que.push({s, 0});
	while (!que.empty()) {
		node t = que.top();
		que.pop();
		if (ans[t.now] != 0x3f3f3f3f) continue;
		ans[t.now] = t.dist;
		for (int i = 1; i <= n; i++) {
			if (dis[t.now][i] != 0x3f3f3f3f) {
				que.push({i, t.dist + dis[t.now][i]});
			}
		}
	}
	for (int i = 1; i <= n; i++) {
		if (i != 1) cout << " ";
		if (ans[i] == 0x3f3f3f3f) {
			cout << 0x7fffffff;
		} else 	cout << ans[i];
	}
	return 0;
}
```

