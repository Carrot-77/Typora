# manacher算法



![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWFnZXMyMDE1LmNuYmxvZ3MuY29tL2Jsb2cvODkwOTY2LzIwMTcwNy84OTA5NjYtMjAxNzA3MjIxNTU2MzA2ODQtMjEzMDAzOTcwNC5wbmc?x-oss-process=image/format,png)

Floyd 多源

Dijkstra 单源， 不能有负权边

Bellman-Ford 速度玄学

A*算法



luogu 1144

```
#include <iostream>

#include <vector>
#include <cmath>
#include <cstring>
#include <algorithm>
#include <map>
#include <queue>
#include <iomanip>
using namespace std;

struct edge {
	int to, val, next;
};

struct node {
	int now, val;
	bool operator< (const node &b) const {
		return this->val > b.val;
	}
};

edge edg[4000005];
int n, m, edg_cnt, head[1000005], ans[1000005], ans_cnt[1000005];

int main() {
	memset(head, -1, sizeof (head));
	memset(ans, 0x3f, sizeof(ans));
	memset(ans_cnt, 0, sizeof(ans_cnt));
	cin >> n >> m;
	for (int i = 0; i < m; i++) {
		int a, b;
		cin >> a >> b;
		edg[edg_cnt].to = b;
		edg[edg_cnt].val = 1;
		edg[edg_cnt].next = head[a];
		head[a] = edg_cnt;
		edg_cnt++;
		edg[edg_cnt].to = a;
		edg[edg_cnt].val = 1;
		edg[edg_cnt].next = head[b];
		head[b] = edg_cnt;
		edg_cnt++;
	}

	priority_queue<node> que;
	que.push({1, 0});
	ans[1] = 0;
	ans_cnt[1] = 1;
	while (!que.empty()) {
		node temp = que.top();
		que.pop();
		if (temp.val > ans[temp.now])
			continue;
		for (int cnt = head[temp.now]; cnt != -1; cnt = edg[cnt].next) {
			if (ans[edg[cnt].to] > temp.val + edg[cnt].val) {
				ans[edg[cnt].to] = temp.val + edg[cnt].val;
				ans_cnt[edg[cnt].to] = ans_cnt[temp.now];
				que.push({edg[cnt].to, ans[edg[cnt].to]});
			} else if (ans[edg[cnt].to] == temp.val + edg[cnt].val) {
				ans_cnt[edg[cnt].to] += ans_cnt[temp.now];
				ans_cnt[edg[cnt].to] %= 100003;
			}
		}
	}
	for (int i = 1; i <= n; i++) {
		cout << ans_cnt[i] << endl;
	}

	return 0;
}

```



luogu 1629

```
#include <iostream>

#include <vector>
#include <cmath>
#include <cstring>
#include <algorithm>
#include <map>
#include <queue>
#include <iomanip>
using namespace std;

struct Edge {
	int to, val, next;
};

struct node {
	int now, val;
	bool operator < (const node &b) const {
		return this->val > b.val;
	}
};

int n, m, head1[1005], head2[1005], ans1[1005], ans2[1005];
Edge edg1[100005], edg2[100005];

int main() {
	memset(head1, -1, sizeof(head1));
	memset(head2, -1, sizeof(head2));
	memset(ans1, 0x3f, sizeof(edg1));
	memset(ans2, 0x3f, sizeof(edg2));
	cin >> n >> m;
	for (int i = 0; i < m; i++) {
		int a, b, c;
		cin >> a >> b >> c;
		edg1[i].to = b;
		edg1[i].val = c;
		edg1[i].next = head1[a];
		head1[a] = i;
		edg2[i].to = a;
		edg2[i].val = c;
		edg2[i].next = head2[b];
		head2[b] = i;
	}
	priority_queue<node> que;
	que.push({1, 0});
	ans1[1] = 0;
	while (!que.empty()) {
		node temp = que.top();
		que.pop();
		if (temp.val > ans1[temp.now]) {
			continue;
		}
		for (int cnt = head1[temp.now]; cnt != -1; cnt = edg1[cnt].next) {
			if (ans1[edg1[cnt].to] > temp.val + edg1[cnt].val) {
				ans1[edg1[cnt].to] = temp.val + edg1[cnt].val;
				que.push({edg1[cnt].to, ans1[edg1[cnt].to]});
			}
		}
	}
	que.push({1, 0});
	ans2[1] = 0;
	while (!que.empty()) {
		node temp = que.top();
		que.pop();
		if (temp.val > ans2[temp.now]) {
			continue;
		}
		for (int cnt = head2[temp.now]; cnt != -1; cnt = edg2[cnt].next) {
			if (ans2[edg2[cnt].to] > temp.val + edg2[cnt].val) {
				ans2[edg2[cnt].to] = temp.val + edg2[cnt].val;
				que.push({edg2[cnt].to, ans2[edg2[cnt].to]});
			}
		}
	}
	int ans = 0;
	for (int i = 2; i <= n; i++) {
		ans += ans1[i] + ans2[i];
	}
	cout << ans << endl;

	return 0;
}

```



