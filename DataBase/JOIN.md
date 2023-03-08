조인
=
- 조인이란 하나의 테이블이 아닌 두 개이상의 테이블을 묶어서 하나의 결과물을 만드는 것을 말합니다.
- MySQL에서는 JOIN을 이용하고, MongoDB에서는 lookup이라는 쿼리로 이를 처리할 수 있습니다.
- MongoDB에서는 lookup을 최대한 사용하지 말아야 합니다. MongoDB에서의 조인 연산에 대해 관계형 데이터베이스보다 성능이 떨어집니다.
- 따라서 조인이 많은 경우 관계형 데이터베이스를 사용하는 것이 좋습니다.
- 조인의 종류
  - 조인의 종류에는 내부조인, 왼쪽 조인, 오른쪽 조인, 합집합 조인이 있습니다.
  - 내부조인 (inner join)
    - 왼쪽 테이블과 오른쪽 테이블의 두 행이 모두 일치한 행만을 표기
    - 두 테이블의 교집합을 나타냅니다.
    ```
    SELECT * FROM tablea A
    INNER JOIN tableb B ON
    A.key = B.key
    ```
  - 왼쪽 조인(left outer join) 
    - 왼쪽 테이블의 모든 행의 결과 테이블에 표기합니다.
    - 왼쪽 조인은 테이블 B의 일치하는 부분의 레코드와 함께 테이블 A를 기준으로 완전한 레코드 집합을 생성합니다.
    - 만약 테이블 B에 일치하는 항목이 없으면 해당 값은 null 값이 됩니다.
    ```
    SELECT * FROM tablea A
    LEFT JOIN tableb B ON
    A.key = B.key
    ```
  - 오른쪽 조인(right outer join)
    - 오른쪽 테이블의 모든 행이 결과 테이블에 표기 됩니다.
    - 왼쪽 조인과 반대로 테이블 B를 기준으로 완전한 레코드 집합을 생성합니다.
    - 만약 테이블 A에 일치하는 항목이 없다면 해당 값은 null 값이 됩니다.
    ```
    SELECT * FROM tablea A
    RIGHT JOIN tableb B ON
    A.key = B.key
    ```
  - 합집합 조인(full outer join)
    - 두 개의 테이블을 기반으로 조인 조건에 만족ㅎ하지 않는 행까지 모두 표기합니다.
    - 합집합 조인(완전 외부 조인)은 양쪽 테이블에서 일치하는 레코드와 함께 테이블 A와 테이블 B의 모든 레코드 집합을 생성합니다. 이때 일치하는 항목이 없으면 누락된 쪽에는 null 값이 포함되어 출력됩니다.
    ```
    SELECT * FROM tablea A
    FULL OUTER JOIN tableb B ON
    A.key = B.key
    ```
