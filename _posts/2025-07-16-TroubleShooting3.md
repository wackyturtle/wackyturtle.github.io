---
layout: single
title: "스파르타 내일배움 캠프 플러터 개인 과제 트러블슈팅"
date: 2025-07-16 10:00:00 +0900
categories: [TroubleShooting, all]
classes: wide
sidebar:
    nav: "counts"
---
<br><br>
# 플러터 개인과제 트러블슈팅

## 엄청나게 다양하고 많은 함수를 어떻게 적재적소에 쓰는가??

### ElevatedButton의 style에 왜 `styleFrom()`을 쓰는가?

![1](/assets/images/트러블슈팅/1.png)  

Flutter에서 `ElevatedButton`의 `style` 매개변수에 값을 줄 때 헷갈릴 수 있는 대표적인 상황:

---

##  상황 요약

- `ElevatedButton` 위젯은 `style`이라는 매개변수를 받음.
- 이 `style`의 타입은 `ButtonStyle`.
- 그런데 막상 스타일을 줄 땐 `ButtonStyle(...)`이 아니라
   `ElevatedButton.styleFrom(...)`을 써야 함.

---

## 초보자가 여기서 헷갈리는 이유

```dart
ElevatedButton(
  style: ButtonStyle( // <- 이렇게 쓰고 싶지만 어렵다!
    backgroundColor: MaterialStateProperty.all(Colors.purple),
  ),
)
```

하지만 이건 너무 복잡해서 초보자에겐 비효율적임.

---

## 그래서 등장한 `styleFrom()`

```dart
ElevatedButton(
  style: ElevatedButton.styleFrom(
    backgroundColor: Colors.purple,
  ),
)
```

이건 내부적으로 `ButtonStyle`을 만들어서 리턴해주는 도우미 함수.
> 결국 `style: ElevatedButton.styleFrom(...)` 도 **타입은 맞게 주는 것**이다.

---

## 직접 타입 확인하고 쓰는 팁

1. `style:` 매개변수 위에 마우스를 올려보자.
   - 주석으로 `styleFrom()` 쓰라는 힌트가 적혀 있을 수 있음.
2. `ButtonStyle` 이름에 `Ctrl + 클릭` (또는 Cmd + 클릭)
   - 정의 내부에 `factory` 생성자나 `static` 메서드를 확인

---

## 요약

| 방법 | 설명 |
|------|------|
| `ButtonStyle(...)` | 직접 스타일을 만드는 기본 생성자. 초보자에게는 다소 어려움. |
| `ElevatedButton.styleFrom(...)` | 간단한 스타일링을 위한 도우미 함수. 내부적으로 `ButtonStyle`을 리턴함. |

---

## 결론

`styleFrom()`은 **편리한 지름길**이며, 내부적으로는 `ButtonStyle`을 생성해주므로 타입도 정확히 맞는다!

![2](/assets/images/트러블슈팅/2.png)   
- 이것도 마찬가지로 결국 알고있는걸 쓰거나
- 구글에 내가 원하는 것의 키워드를 검색해서 찾아보거나
- 정의부분 들어가서 삽질하면서 찾아보거나
- 그냥 삽질해보거나
- 그게 답이다 편한길은 없다고 한다..










