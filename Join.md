# Join 이란

> 조인이란 여러 테이블에 흩어져 있는 정보 중 사용자가 필요한 정보만 가져온뒤 가상의 테이블처럼 만들어서 결과를 보여주는 것으로 2개의 테이블을 조합하여 하나의 열로 표현하는 것이다.

#### Join의 종류로는 크게 2가지가 있다.

1. INNER JOIN
2. OUTER JOIN

---

## INNER JOIN

> Inner Join은 키 값이 있는 테이블의 컬럼 값을 비교 후 조건에 맞는 값을 가져오는 것이다.(서로 연관된 내용을 검색해 값을 가져오는 조인 방법이다.)

![INNER JOIN](https://t1.daumcdn.net/cfile/tistory/251A374456EB994D13)

다음 예제는 `user` 테이블과 `post` 테이블을 INNER JOIN하는 쿼리문이다.

```mysql
select * from user join post on user.id=post.user_id;
```

**이 쿼리문은 user테이블의 id와 post테이블의 user_id가 같은 데이터를 반환한다.(단 만약 user가 post를 갖지 않았다면 데이터를 가져오지 않는다.)**



## OUTER JOIN

> Outer Join은 조인하는 여러 테이블에서 한 쪽에는 데이터가 있고 한 쪽에는 데이터가 없는 경우, 데이터가 있는 쪽 테이블의 내용을 전부 출력하는 방법이다.(조인의 조건이 만족하지 않아도 해당 행을 출력하고 싶을 때 사용한다.)

#### OUTER JOIN의 종류는 3가지가 있다.

1. LEFT OUTER JOIN
2. RIGHT OUTER JOIN
3. PULL OUTER JOIN



##### Left Outer Join

> Left Outer Join은 조인문의 왼쪽에 있는 테이블의 모든 결과를 가져온 후 오른쪽 테이블의 결과를 매칭하고, 매칭되는 데이터가 없는 경우 NULL을 표시한다.

![LEFT OUTER JOIN](https://t1.daumcdn.net/cfile/tistory/224EFA4656EF49B309)

다음 예제는 `user` 테이블과 `post` 테이블을 LEFT OUTER JOIN하는 쿼리문이다.

```mysql
select * from user left join post on user.id=post.user_id; 
```

**이 쿼리문은 user테이블의 모든 데이터와, user.id와 post.user_id가 같은 데이터를 반환한다.(단 user가 post를 갖지 않은 상태라면 join된 post데이터는 NULL로 표시된다.)**



##### Right Outer Join

> Right Outer Join은 조인문의 오른쪽에 있는 테이블의 모든 결과를 가져온 후 왼쪽의 테이블의 데이터를 매칭하고, 매칭되는 데이터가 없는 경우 NULL을 표시한다.

![Right Outer Join](https://t1.daumcdn.net/cfile/tistory/2418A25056EF4BA912)

```mysql
select * from user right join post on user.id=post.user_id;
```

**이 쿼리문은 post테이블의 모든 데이터와, user.id와 post.user_id가 같은 데이터를 반환한다.(단 post가 user를 갖지 않은 상태라면 join된 user데이터는 NULL로 표시된다.)**



##### Full Outer Join

> Full Outer Join은 Left Outer Join과 Right Outer Join을 합친 것으로, 양쪽 모두 조건이 일치하지 않는 것들까지 모두 결합하여 출력한다.

![Pull Outer Join](https://t1.daumcdn.net/cfile/tistory/232EF54356EF4DA123)

```mysql
select * from user left join post on user.id=post.user_id
union
select * from user right join post on user.id=post.user_id;
```

**MySQL에서는 Full Outer Join을 지원하지 않는다. 그래서 MySQL의 UNION기능을 사용해, Full Outer Join을 사용할 수 있다.**