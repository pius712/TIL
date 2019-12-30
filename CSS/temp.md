높이가 같은 경우에는 굳이 가로, 세로로 나눌 필요가 없다. 예를 들어서 네이버의 뉴스 스탠드의 언론사 목록같은 경우에는 높이가 모두 같기 때문에 incline으로 해둬 자동으로 격자모양으로 찬다. 

아래의 `div` 두개가 세로 배치가 안맞을때 vertical align 주면 된다. 

```HTMLx
    <div>
        <div></div>
        <div></div>
    </div>
```

inline-block의 문제점? 

nth-of-type vs nth-child 

내부 컨텐츠의 가로 정렬을 text-align: center
세로 정렬은 컨텐츠에

```CSS
position: relative;
top:50%;
transform: translateY(-50%);
```
  
top 50%를 하면 기준이 끝이라서 중간보다 아래에 있어보인다. 그런데 translateY(-50%) 하면 이미지 크기의 반절만큼을 위로 올려준다. 