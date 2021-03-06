import heapq
import datetime
from collections import defaultdict

n, m = [int(_) for _ in input().split()]
mp = defaultdict(list)
for _ in range(m):
    u, v, time = [int(_) for _ in input().split()]
    mp[u].append((v, time))
    mp[v].append((u, time))
s, e, start = input().split()
s, e = int(s), int(e)


def dijkstra():
    pq = [(0, s)]
    dist = {}
    while pq:
        d, node = heapq.heappop(pq)
        if node in dist: continue
        dist[node] = d
        for nei, d2 in mp[node]:
            if nei not in dist:
                heapq.heappush(pq, (d + d2, nei))
    return dist[e]


cur_year = "2020"
hours = dijkstra()
d = datetime.datetime.strptime(cur_year + "/" + start, "%Y/%m.%d/%H")
delta = datetime.timedelta(hours=hours)
d += delta
# print(datetime.datetime.strftime(d, "%-m.%-d/%H"))
print("{}.{}/{}".format(d.month, d.day, d.hour))



from queue import PriorityQueue
from collections import defaultdict


def prim():
    q = PriorityQueue()
    vis = [False for _ in range(n + 1)]
    vis[0] = True
    q.put((0, 1))
    ret = 0
    while not q.empty():
        e, u = q.get()
        if vis[u]:
            continue
        if e > k:
            return False
        vis[u] = True
        ret += e
        for v, w in mp[u]:
            if not vis[v]:
                q.put((w, v))
    if all(vis):
        return True
    else:
        return False


ans = []
T = int(input())
for _ in range(T):
    n, m, k = [int(_) for _ in input().split()]
    mp = defaultdict(list)
    for _ in range(m):
        u, v, w = [int(_) for _ in input().split()]
        mp[u].append((v, w))
        mp[v].append((u, w))
    if prim():
        print("Yes")
    else:
        print("No")
        
        
from collections import defaultdict
import heapq


def prim():
    vis = set()
    q = []
    heapq.heappush(q, (0, 1))
    while q:
        e, u = heapq.heappop(q)
        if u in vis:
            continue
        if e > k:
            return False
        vis.add(u)
        for v, w in mp[u]:
            if v not in vis:
                heapq.heappush(q, (w,v))
    if len(vis) == n:
        return True
    else:
        return False

T = int(input())
for _ in range(T):
    n, m, k = [int(_) for _ in input().split()]
    mp = defaultdict(list)
    for _ in range(m):
        u, v, w = [int(_) for _ in input().split()]
        mp[u].append((v, w))
        mp[v].append((u, w))
    if prim():
        print("Yes")
    else:
        print("No")
