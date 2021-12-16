## preview
인접행렬을 사용하는 연결요소 카운팅 문제. 인접리스트를 더 많이 사용했기에 인접행렬 연습겸으로 풀어봤다.
    
    
## n*n 인접 행렬 입력받기.

```
int grp[1001][1001];

for (int i=0; i<n; i++)
{
  string a; cin >> a;
  for(int j=0; j<n; j++)
  {
    grp[i][j] = a[j] - '0';
  }
}
```
    
     
## vector 사용시 주의점.

항상 vector접근 전에 resize()를 이용하여 메모리를 할당하자. 밑의 코드처럼 할당하지 않고 접근시 런타임에러가 발생한다.

```
#include <bits/stdc++.h>
using namespace std;

vector <int> v;

int main()
{
    v[0] = 0;
    v[1] = 1;
    v[2] = 2;
    
    v.resize(3);
    
    for (int i=0; i<3; i++) cout << v[i] << '\n';
    
    return 0;
}
```
    
    
## 인접행렬 dfs코드

```
int dx[4] = {-1, 0, 1, 0};
int dy[4] = {0, -1, 0, 1};

void dfs(int y, int x)
{
    visited[y][x] = 1;
    for (int i=0; i<4; i++)
    {
        int nx = x + dx[i]; int ny = y + dy[i];
        if ((0 <= ny && ny < n) && (0 <= nx && nx < n) && !visited[ny][nx] && grp[ny][nx]) dfs(ny, nx);
    }
}
```
      
      
## 해결

```
#include <bits/stdc++.h>
using namespace std;

int grp[26][26];
int visited[26][26];

vector<int> res;

int dx[4] = {-1, 0, 1, 0};
int dy[4] = {0, -1, 0, 1};

int n;
int c_cmpnt = 0;
int v = 0; 

void dfs(int y, int x)
{
    v++;
    visited[y][x] = 1;
    for (int i=0; i<4; i++)
    {
        int nx = x + dx[i]; int ny = y + dy[i];
        if ((0 <= ny && ny < n) && (0 <= nx && nx < n) && !visited[ny][nx] && grp[ny][nx]) dfs(ny, nx);
    }
}


int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    
    cin >> n;
    
    for (int i=0; i<n; i++)
    {
        string a; cin >> a;
        for (int j=0; j<n; j++)
        {
            grp[i][j] = a[j] - '0';
        }
    }
    
    res.resize(100000);
    
    for (int i=0; i<n; i++)
    {
        for (int j=0; j<n; j++)
        {
            if (!visited[i][j] && grp[i][j])
            {
                dfs(i, j);
                res[c_cmpnt] = v;
                c_cmpnt++;
                v = 0;
            }
        }
    }
    
    res.resize(c_cmpnt);
    sort(res.begin(), res.end());
    
    cout << c_cmpnt << '\n';
    for (int i=0; i<c_cmpnt; i++) cout << res[i] << '\n';
    
    
    return 0;
}
```



  
