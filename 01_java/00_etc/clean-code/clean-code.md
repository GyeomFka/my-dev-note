목차
--------
1. 클린코드란 무엇인가? by 오브젝트 벤토 진영
2. 클린코드가 필요한 이유?
3. 클린코드를 학습하는 방법
---
1) 네이밍의 의도를 밝혀라
```java
//나쁜예
public class CleanCode{
    public List<int[]> getThem() {
    	List<int[]> list = new ArrayList<int[]>();
    
    	for (int[] x : theList) {
    		if (x[0] == 4) {
    			list.add(x);
    		}
    	}
		return list;
    }
}
```
```java
//좋은예
public class CleanCode {
	public List<int[]> getFlaggedCells() {
		List<int[]> flaggedCells = new ArrayList<int[]>();

		for (int[] cell : theGameBoard) {
			if (cell[STATUS] == FLAGGED) {
				flaggedCells.add(cell);
			}
		}
		return flaggedCells;
	}
}
```
  - 해당 리스트가 `무슨 객체`를 담은 리스트인지, 분기문이 어떤 `상황`에 분기를 하는지 속성의 의도를 밝히자
2) 그릇된 정보를 피하라 
   - user를 반환하면 user를 반환하자
3) 이름을 의미있게 구분하라
   - User -> UserDetail, UserInfo -> UserDetailInfo
4) 검색하기 쉬운 이름을 사용하자
   - product -> prdt 식의 줄임 자제
5) 클래스 이름, 메서드 이름
   - 클래스 : 명사
   - 메서드 : 동사
6) 한 개념에 한 단어를 사용하라
   - User, Member, Client 헷갈린다. 통일을 하자
7) 함수 코딩방법
   1) 작게 만들자, 더 작게 만들자
   2) 한 가지 일만 하자, 그 한가지를 더 잘 해야 한다.
   3) 함수 당 추상화 수준은 하나다
   4) 함수의 인수 갯수를 최대한 줄이자
      1) 인수가 늘어나면, 객체나 DTO를 사용하자
   5) 반복하지마라
      1) DRY - Do not Repeat Yourself
   6) 주석은 최소화, 변수 네이밍을 최대
   7) 형식 맞추기(convention)
      1) 적절한 행 길이 유지
         1) 신문기사처럼 작성하라 -> 위에서 아래
         2) 개념은 빈 행으로 분리하라
         3) 세로 밀집도
         4) 수직 거리 - 서로 밀접한 개념은 가깝게