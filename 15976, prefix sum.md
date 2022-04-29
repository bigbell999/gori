## 핵심코드

```c++
y_idx.resize(m+1); sum.resize(m+1);
    for (int i=0; i<m; i++)
    {
        cin >> idx >> value;
        y_idx[i] = idx;
        sum[i+1] = sum[i] + value;
    }
    y_idx[m] = 1e18;
    //1e18은 double 형식의 1*10**18이다.
```
부분합 구하기 빌드업. 활용할 곳이 많을 것 같다. 
만약 idx a부터 idx b까지의 부분합을 알고싶다면,

  sum[b+1] - sum[a];
  


## 실수

```c++
for (int i=0; i<n; i++)
    {
        ll high = upper_bound(y_idx.begin(), y_idx.end(), x_idx[i] + b) - y_idx.begin();
        ll low = lower_bound(y_idx.begin(), y_idx.end(), x_idx[i] + a) - y_idx.begin();
        ll tmp = x[i] * (sum[high]- sum[low]);
        res += tmp;
    }
```

처음 코드는
```c++
  ll high = lower_bound(y_idx.begin(), y_idx.end(), x_idx[i] + b) - y_idx.begin();
  ll tmp = x[i] * (sum[high+1] - sum[low];
```
이렇게 되면, 찾으려는 값(여기서는 x_idx[i] + b)가 없을 경우 찾으려는 값을 두번째로 초과하는 값의 index가 high로 들어가는 오류가 생김.
  
