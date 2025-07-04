---
layout: single
title: "스파르타 내일배움 캠프 개인 심화과제 트러블슈팅"
date: 2025-07-04 10:00:00 +0900
categories: [TroubleShooting, all]
classes: wide
sidebar:
    nav: "counts"
---
<br><br>
## 정상적이지 않은 종료
**monsterList**의 **length**만큼 수행되면 프로그램이 종료되어야 하는데,  
문제는 한번 수행이 될때마다 **monsterList**의 **length**값이 줄어들기 때문에  
오류가 났다  

해결방법은  
첫 **monsterList**의 **length**의 값을 저장해놓는 변수 **monsterListLength**를 만들어줘서 해결했다  

```dart
int monsterListLength = 0;

if (point == monsterListLength) {
	endGame(true);
}
```
<br><br>
## Nullable and NullCheck
아직까지 정말 익숙치 않치만 그래도 익숙해져야만 하는 Nullable..  
```dart
String? y_or_n = 'p';

stdout.write('다음 몬스터와 싸우시겠습니까? (y / n):');
      while (y_or_n != 'y') {
        y_or_n = stdin.readLineSync();
        if (y_or_n != null && y_or_n.isNotEmpty) {
          if (y_or_n == 'y') {
            break;
          } else if (y_or_n == 'n') {
            endGame(false);
          } else {
            print('올바른 값을 입력하세요.');
          }
        }
      }
```
위와 같은 경우에도 난 대충 **String y_or_n**를 입력받아서 쓰고 싶은데,  

**readLineSync**()를 사용할려면 입력값이 **null**일 수도 있기때문에  
그냥 **String** 을 쓰면 안되고 **String**?을 쓰거나,  
**stdin.readLineSync()!** 이런식으로 문법을 구성해줘야하는 부분이 참 익숙치 않다.  

아직까진 어느 상황에 어떤 것이 더 나은 **nullable**처리법인지 잘 구분이 안간다만  
하다보면 느낌이 올거라고 생각한다.  

그리고 널 체크도 익숙해질때 까진   
**if (y_or_n != null && y_or_n.isNotEmpty)**{}를 자주 쓰게 될 것 같다.  
가장 무난하고 많이 쓰일 것 같다.  


<br><br>
<br><br>


솔직히 그 외에도 많은 사소한 문제들이 있었지만 금방 해결돼서 넘어가거나  
아니면 너무 집중해서 기록할 겨를이 없이 고민하다가 넘어간게 많아서 기억이 잘  
안난다..;;^^  
아직 깃허브 커밋같은 프로젝트 내용이 크지않다 보니 필요성을 못 느껴  
많이 안하게 되는 경향이 있는데,  
앞으로는 이슈가 발생하면 미리 적어놔서 트러블슈팅을 기록한다던지,  
깃허브 커밋을 자주 이용해본다던지 하면 더 좋을 것 같다는 생각이 든다.  
