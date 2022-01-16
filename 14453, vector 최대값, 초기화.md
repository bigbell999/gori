## preview
dp로 간단하게 풀 수 있는 문제이다. 그런데 내가 vector를 다루는 지식이 부족하여 최대값을 찾는 코드를 짜기가 어려웠다.     

시간이 오래걸렸지만 그만큼 배운 것도 많은 문제이다.   

## 1트

```
#include <bits/stdc++.h>
using namespace std;

int n;
vector<int> hps;
vector<int> res;
int a[100002][3];
int b[100002][3];

int max3(int arr[3])
{
    int m = 0;
    for (int i=0; i<2; i++)
    {
       if (arr[i] > m) m = arr[i];
    }
    
    return m;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    
    cin >> n;
    if (n==1)
    {
        cout << 1;
        return 0;
    }
    hps.resize(n); res.resize(n);
    
    //입력
    char hand;
    for (int i=0; i<n; i++)
    {
        cin >> hand;
        if (hand == 'H') hps[i] = 0;
        else if (hand == 'P') hps[i] = 1;
        else if (hand == 'S') hps[i] = 2;
    }
    
    //초기설정
    for (int i=0; i<n; i++) b[0][hps[i]]++;
    res[0] = max3(b[0]);
    
    //dp
    for (int i=0; i<n-1; i++)
    {
        a[i+1][0] = a[i][0]; a[i+1][1] = a[i][1]; a[i+1][2] = a[i][2];
        b[i+1][0] = b[i][0]; b[i+1][1] = b[i][1]; b[i+1][2] = b[i][2];
        
        a[i+1][hps[i]] = a[i][hps[i]] + 1;
        b[i+1][hps[i]] = b[i][hps[i]] - 1;
        res[i+1] = max3(a[i+1]) + max3(b[i+1]);
    }
    
    int ans = 0;
    for (int i=0; i<n; i++)
    {
        if (res[i] > ans) ans = res[i];
    }
    cout << ans;
    
    return 0;
}
```

핵심은 역시 dp부분

```
//dp
    for (int i=0; i<n-1; i++)
    {
        a[i+1][0] = a[i][0]; a[i+1][1] = a[i][1]; a[i+1][2] = a[i][2];
        b[i+1][0] = b[i][0]; b[i+1][1] = b[i][1]; b[i+1][2] = b[i][2];
        
        a[i+1][hps[i]] = a[i][hps[i]] + 1;
        b[i+1][hps[i]] = b[i][hps[i]] - 1;
        res[i+1] = max3(a[i+1]) + max3(b[i+1]);
    }
```

계속 틀리길래 이 쪽 코드가 틀린 줄 알고 많이 해맸다.

## 성공

```
#include <bits/stdc++.h>
using namespace std;

int n;
vector<int> hps;
vector<int> res;
vector<vector<int>> a(100002, vector <int>(3, 0));
vector<vector<int>> b(100002, vector <int>(3, 0));

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    
    cin >> n;
    hps.resize(n); res.resize(n);
    a.resize(n); b.resize(n);
    
    
    //예외 처리
    if (n==1)
    {
        cout << 1;
        return 0;
    }
    
    //입력
    char hand;
    for (int i=0; i<n; i++)
    {
        cin >> hand;
        if (hand == 'H') hps[i] = 0;
        if (hand == 'P') hps[i] = 1;
        if (hand == 'S') hps[i] = 2;
    }
    
    //초기설정
    for (int i=0; i<n; i++) b[0][hps[i]]++;
    res[0] = *max_element(b[0].begin(), b[0].end());
    
    //dp
    for (int i=0; i<n-1; i++)
    {
        a[i+1][0] = a[i][0]; a[i+1][1] = a[i][1]; a[i+1][2] = a[i][2];
        b[i+1][0] = b[i][0]; b[i+1][1] = b[i][1]; b[i+1][2] = b[i][2];

        a[i+1][hps[i]] = a[i][hps[i]] + 1;
        b[i+1][hps[i]] = b[i][hps[i]] - 1;
        res[i+1] = *max_element(a[i+1].begin(), a[i+1].end()) + *max_element(b[i+1].begin(), b[i+1].end());
    }
    
    //결과 
    int ans = *max_element(res.begin(), res.end());
    cout << ans;
    
    return 0;
}
```

### 새로 배운 것

1. vector에서 최대, 최소값 찾기

```
//최대값
int max = *max_element(v.begin(), v.end());

//최소값
int min = *min_element(v.begin(), v.end());
```
      
      
2. vector 초기화

```
//n개의 원소를 추가하고 모두 0으로 초기화.
vector<int> v(n, 0);
```

아마도 처음 코드는 초기화가 안된 원소에 접근하여 비교연산자를 사용했기 때문에 오류가 생긴 듯 하다.

