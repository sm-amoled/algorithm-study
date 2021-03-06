# 쇠막대기

문제 번호: 10799
알고리즘 분류: 스택
푼 날짜: 2021년 2월 10일 오후 10:03

## 문제링크

[https://www.acmicpc.net/problem/10799](https://www.acmicpc.net/problem/10799)

## 문제

여러 개의 쇠막대기를 레이저로 절단하려고 한다. 효율적인 작업을 위해서 쇠막대기를 아래에서 위로 겹쳐 놓고, 레이저를 위에서 수직으로 발사하여 쇠막대기들을 자른다. 쇠막대기와 레이저의 배치는 다음 조건을 만족한다.

- 쇠막대기는 자신보다 긴 쇠막대기 위에만 놓일 수 있다. - 쇠막대기를 다른 쇠막대기 위에 놓는 경우 완전히 포함되도록 놓되, 끝점은 겹치지 않도록 놓는다.
- 각 쇠막대기를 자르는 레이저는 적어도 하나 존재한다.
- 레이저는 어떤 쇠막대기의 양 끝점과도 겹치지 않는다.

아래 그림은 위 조건을 만족하는 예를 보여준다. 수평으로 그려진 굵은 실선은 쇠막대기이고, 점은 레이저의 위치, 수직으로 그려진 점선 화살표는 레이저의 발사 방향이다.

![https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/problem/10799/1.png](https://onlinejudgeimages.s3-ap-northeast-1.amazonaws.com/problem/10799/1.png)

이러한 레이저와 쇠막대기의 배치는 다음과 같이 괄호를 이용하여 왼쪽부터 순서대로 표현할 수 있다.

1. 레이저는 여는 괄호와 닫는 괄호의 인접한 쌍 ‘( ) ’ 으로 표현된다. 또한, 모든 ‘( ) ’는 반드시 레이저를 표현한다.
2. 쇠막대기의 왼쪽 끝은 여는 괄호 ‘ ( ’ 로, 오른쪽 끝은 닫힌 괄호 ‘) ’ 로 표현된다.

위 예의 괄호 표현은 그림 위에 주어져 있다.

쇠막대기는 레이저에 의해 몇 개의 조각으로 잘려지는데, 위 예에서 가장 위에 있는 두 개의 쇠막대기는 각각 3개와 2개의 조각으로 잘려지고, 이와 같은 방식으로 주어진 쇠막대기들은 총 17개의 조각으로 잘려진다.

쇠막대기와 레이저의 배치를 나타내는 괄호 표현이 주어졌을 때, 잘려진 쇠막대기 조각의 총 개수를 구하는 프로그램을 작성하시오.

## 입력

한 줄에 쇠막대기와 레이저의 배치를 나타내는 괄호 표현이 공백없이 주어진다. 괄호 문자의 개수는 최대 100,000이다.

## 출력

잘려진 조각의 총 개수를 나타내는 정수를 한 줄에 출력한다.

## 조건

- 시간 제한 : 1s
- 메모리 제한 : 256MB

---

## 해설

(이 연속으로 나올 때는 쇠파이프가 추가될 때, )이 연속으로 나올 때는 쇠파이프가 끝날 때, ()이 한 번에 나올 때는 레이저로 자르는 때이다. 이 점을 이용해 문제를 해결하면 된다.

## 풀이

문자열의 형태로 입력되기 때문에, string 타입으로 입력받은 뒤 null 문자가 나올 때 까지 한 글자씩 잘라 판단하였다.

`cutCount`는 현재 자르면 추가되는 쇠파이프 조각의 수를 의미한다. `cutSum`은 현재까지 얻은 쇠파이프 조각의 수를 의미한다. 쇠파이프를 자르면 `cutCount`만큼 `cutSum`에 값이 추가된다. 읽은 문자가 ‘(‘인 경우, 바로 뒤 문자가 ‘)’라면 절단하는 포인트이므로, `cutSum += cutCount`를 해준다.

```cpp
if(N[index] == '(') {
    if(N[index + 1] == '(') {
        cutCount++;
        index++;
    } else {
				// () 둘을 한 번에 비교하였으므로 index를 2 증가시킨다.
        cutSum += cutCount;
        index += 2;
    }
} else {
    cutCount--;
		// 파이프가 끝날 때에도 원래 있던 파이프의 수를 더해준다.
    cutSum++;
    index++;
}

```

모든 문자에 대해 위 코드를 처리하고 cutSum을 출력하면 원하는 결과를 얻을 수 있다.

---

## 코멘트

아직까지는 간단한 문제들인 것 같네! 

---

## 코드

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int main() {
    string N;
    cin >> N;
    
    int index = 0;
    
    int cutCount = 0;
    long cutSum = 0;
    while(N[index] != 0) {
        if(N[index] == '(') {
            if(N[index + 1] == '(') {
                cutCount++;
                index++;
            } else {
                cutSum += cutCount;
                index += 2;
            }
        } else {
            cutCount--;
            cutSum++;
            index++;
        }
    }
    
    cout << cutSum;
       
    return 0;
}
```