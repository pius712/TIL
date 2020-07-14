# infinite scroll

페이스북, 유튜브, 트위터에서 스크롤을 내리면 특정 지점에서 post를 로딩하는 기술이다.

이를 구현하는 방법.

- window.scrollY
- element.clientHeight
- element.scorllHeight
- 인피니트 스크롤 구현

## window.scrollY

Window 인터페이스의 scrollY 읽기 전용 속성은 문서가 수직으로 얼마나 스크롤됐는지 픽셀 단위로 반환합니다. 최신 브라우저에서는 값의 정밀도가 픽셀보다 작으므로 반드시 정숫값을 반환하는건 아닙니다. 

원점으로부터 문서를 수직방향으로 스크롤한 픽셀의 수를 나타내는, 배정밀도 부동소수점 값. 양의 값이 위쪽 스크롤을 의미합니다. 문서를 단일 픽셀보다 높은 정밀도의 장치에서 렌더링한 경우 반환값의 정밀도도 높아져 소숫값을 반환할 수 있습니다. 문서가 위나 아래로 전혀 움직이지 않은 상태면 0을 반환합니다.

---
**note**
정숫값이 필요하면 Math.round()를 사용해 반올림.

---

더 기술적인 용어로, scrollY는 현재 뷰포트 위쪽 모서리의 Y좌표를 반환하고, 뷰포트가 없으면 0을 반환합니다.

## documentElement.clientHeight

읽기 전용 속성인 Element.clientHeight은 엘리먼트의 내부 높이를 픽셀로 반환합니다. 이 내부 높이라는 것은 내부 여백(padding)을 포함하지만, 수평 스크롤바의 높이, 경계선, 또는 외부 여백(margin)은 포함하지 않습니다.

clientHeight는 CSS상의 높이 + CSS상의 내부 여백 - 수평 스크롤바의 높이(존재하는 경우에만)로  계산됩니다.

// 읽기 전용 속성  


The Element.clientHeight read-only property is zero for elements with no CSS or inline layout boxes; otherwise, it's the inner height of an element in pixels. It includes padding but excludes borders, margins, and horizontal scrollbars (if present).
### `document.documentElement.clientHeight`

clientHeight가 root element에 사용된다면, 이 값은 뷰포트의 높이를 반환한다. 따라서 `document.documentElement.clientHeight`의 경우에는 뷰포트의 높이를 나타낸다.  
This is a special case of clientHeight.

## documentElement.scrollHeight

// 읽기 전용 속성  
Element.scrollHeight는 element의 content에 대한 높이 측정 값이다. 여기서 content는 overflow로 인해 screen에 나오지 않는 높이도 포함한다. 

scrollHeight 값은 수직 스크롤 바를 사용하지 않고 모든 content를 뷰포트 내에서 나타낼 수 있는 최소한의 높이이다. 

element의 padding까지 크기를 측정하고, border, margin이나 수평 스크롤바는 포함하지 않는다. 

컨텐츠가 수직 스크롤바가 없이도 화면에 딱 맞게 들어간다면, clientHeight와 같은 값을 가진다. 

### `document.documentElement.scrollHeight`

전체 document의 스크롤을 포함한 가장 위에서부터 가장 아래까지의 height를 반환하게 된다. 

## 인피니트 스크롤 구현

`scrollY + clientHeight = scrollHeight`