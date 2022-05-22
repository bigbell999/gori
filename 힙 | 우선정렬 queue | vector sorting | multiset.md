https://yoongrammer.tistory.com/81    우선정렬 큐          
https://blockdmask.tistory.com/80     multiset container 정리.        
https://breakcoding.tistory.com/117     sort()함수 정리.          

## 힙

### 특징
1. 완전 이진 트리.
2. 부모간의 대소관계 존재, 형제간은 대소관계 존재하지 않음.

          
## 우선정렬 큐

### 특징
1. input 순서에 상관없이 우선순위대로 정렬.        
2. 우선순위가 높은 순서대로 output.            
3. 힙으로 구현 (enqueu, dequeue 모두 logN의 시간복잡도를 보장.)             

## multiset container
1. .insert(key) : insert순서와 상관없이 오름차순 정렬, 시간복잡도 logN (그냥 set은 key값 중복이 안된다.)            
2. .find(key) : key값을 찾아 iterator를 반환, 시간복잡도 logN.          


## sort
1. 배열의 경우

```
sort(arr, arr + size_arr, cmp);
```

2. vecotr의 경우

```
sort(v.begin(), v.end(), cmp);
```

3. 내림차순

```
sort( arr, arr + size_arr, greater<자료형>() );
sort( v.rbegin(), v.rend() );
```

4. 임의기준
sort의 세번째 인자로 함수객체나 함수 포인터를 넣어주면 된다.        
이 함수는 bool값을 반환해야하면 함수 인자 2개를 가져야 한다.           
            
예시
```
bool cmp(int a, int b)
{ 
    return a > b; 
}
```
