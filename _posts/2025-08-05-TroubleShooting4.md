---
layout: single
title: "어렵다 이제 진짜 어렵따;; 개인 과제 트러블슈팅 4"
date: 2025-08-05 10:00:00 +0900
categories: [TroubleShooting, all]
classes: wide
sidebar:
    nav: "counts"
---
<br><br>
# 복습이 너무나도 절실한 과제..

<br><br>

# 1. firebase가 윈도우에서 전역으로 설치되지 않는 오류 발생

- 그래서 로그인이 됐지만 configure을 해도 내 아이디의 프로젝트 파일을 찾지 못함

- 그래서 그냥 node.js 설치 후 npm으로 다운로드

- node.js를 설치하니 chocoletey부터 npm 까지 전부 자동 다운되고,
- 그 뒤로는 강의영상대로 수월하게 진행됨

# 2. Json Type 문제
**Q:** 원래 검색하면 결과값이 나왔는데, repository코드를 수정하고 나니 검색이 먹통이 됐다. 원인이 뭘까?  
**A:**  
- 과제에서 좌표값을 double로 만들라고 해서 난 당연히 Json에서 넘어오는 값도 double일 줄 알았지만
- "mapx": "1269800492"
- "mapy": "375787817" 
- 위 처럼 String값으로 넘어오는걸 몰랐어서 꽤나 헤맸다..
- 다음부턴 받는 값의 타입을 잘 확인해야 할것 같다.  

---


# 3. HTML 태그 제거
**Q:** 검색 API 응답에 `<b>` `</b>` 같은 HTML 태그가 포함돼 있는데 어떻게 제거해?  
**A:**  

## Flutter/Dart `replaceAll`와 `RegExp`를 이용한 HTML 태그 제거 정리

## 1. `replaceAll` 함수의 쓰임과 사용 방법
- **역할**: 문자열에서 특정 부분을 **다른 문자열로 전부 교체**할 때 사용.
- **형식**:
  ```dart
  String replaceAll(Pattern from, String replace)
  ```
  - `from`: 교체할 대상(문자열 또는 정규식 `RegExp`).
  - `replace`: 바꿀 문자열.
- **예시**:
  ```dart
  String text = "Hello <b>World</b>";
  String clean = text.replaceAll("<b>", "").replaceAll("</b>", "");
  print(clean); // Hello World
  ```
  위 예시는 단순 문자열 매칭이므로 `<b>`와 `</b>`만 제거 가능.

---

## 2. `RegExp` 패턴 방식
- **`RegExp`**: Regular Expression(정규식) 패턴을 Dart에서 표현하는 클래스.
- **정규식 기본 형식**:
  ```dart
  RegExp(r'패턴')
  ```
- **특정 패턴 매칭 예시**:
  - `.` → 모든 문자 하나
  - `*` → 앞의 패턴이 0번 이상 반복
  - `[]` → 문자 집합(대괄호 안의 문자 중 하나)
  - `[^ ]` → 대괄호 안 문자를 제외한 모든 문자

---

## 3. `<[^>]*>` 패턴 해석
- `<` : 태그의 시작 기호.
- `[^>]` : **">"가 아닌** 모든 문자.
- `*` : 0번 이상 반복.
- `>` : 태그의 끝 기호.

즉, `<[^>]*>`는 **"<"로 시작하고 ">"로 끝나는 모든 문자열**을 매칭.
- `<b>` → 매칭
- `</b>` → 매칭
- `<div class="test">` → 매칭

이렇게 HTML 태그 전체를 한 번에 제거 가능.

---

## 4. 왜 이걸 사용해야 했는가?
- 네이버 지역 검색 API를 사용했을 때, 응답 JSON의 `title` 값에 `<b>` 태그가 들어오는 경우가 있었음.
  ```json
  {
    "title": "<b>새진흥</b>7차아파트",
    "category": "주택-아파트",
    "roadAddress": "경상남도 양산시 신명2길 16-33"
  }
  ```
- 이 태그는 검색어 하이라이트용이므로 UI에서는 불필요.
- 단순 `replaceAll("<b>", "")`로는 `<b>`와 `</b>`만 제거 가능하고, 다른 HTML 태그가 추가될 경우 대응 불가능.
- 따라서 **정규식 패턴 `<[^>]*>`**를 이용하여 **모든 HTML 태그를 일괄 제거**해야 함.

---

## 5. 최종 해결 코드
```dart
String removeHtmlTags(String htmlText) {
  return htmlText.replaceAll(RegExp(r'<[^>]*>'), '');
}

// 사용 예시
Text(
  removeHtmlTags(location.title),
  style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
);
```

---
