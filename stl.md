vector
-----------------
1. 선언
```
// type안에는 pair나 tuple등도 들어갈 수 있음. 
// 예) vector<pair<int, int>> arr; vector<tuple<int, int, int>> arr;
vector<type> arr;

//n크기 생성가능.
vector<type> arr(n);

//크기 n 0초기화 
vector<type> arr(n, 0);
```

2. 삽입, 삭제
```
// 맨 뒤에 추가
arr.emplace_back(item); 
//arr.push_back(item);

//맨뒤의 원소 삭제
arr.pop_back();
```

3. 크기, 재정의
```
//크기 반환
arr.size();

//크기 n으로 재정의
arr.resize(n);

//크기 n으로 재정의하고, 값을 1로 초기화
arr.resize(n, 1);
```

4. 정렬
```
//오름차순 정렬
sort(arr.begin(), arr.end());

//여기서 compare은 bool값, vector안의 값이 pair등인경우 첫번째 원소가 같을 때 두번째 원소 기준으로 정렬할 수 있게 해줌.
//https://m.blog.naver.com/PostView.nhn?blogId=ckdgus1433&logNo=221666899817&categoryNo=13&proxyReferer=https:%2F%2Fwww.google.com%2F 참고
sort(arr.begin(), arr.end(), compare); 
```

