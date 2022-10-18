# study_sql


## FROM
FROM : 특정 테이블을 호출하는 함수
## SELECT
SELECT : 특정 컬럼을 가져오겠다
- AS : 특정 컬럼의 이름을 변경하여 호출

~~~Ini
SELECT * FROM Customers;
~~~

~~~Ini
SELECT
  CustomerId AS ID,
  CustomerName AS "이름",
  Address AS ADDR
FROM Customers
~~~
한글은 "문자열"

## WHERE
WHERE : 구문 뒤에 조건을 붙여 원하는 데이터만 가져옴
~~~Ini
SELECT * FROM Orders
WHERE EmployeeID = 3;
~~~

## ORDER BY
ORDER BY : 특정 구문을 사용해서 특정 컬럼을 기준으로 데이터를 정렬
- ASC : 오름차순
- DESC : 내림차순

~~~Ini
SELECT * FROM OrderDetails
ORDER BY ProductID ASC, Quantity DESC
~~~
먼저 ProductID를 오름차순으로 정렬 후,
ProductID가 같은 행에서는 Quantity는 내림차순으로 정렬

## LIMIT
LIMIT: 원하는 만큼만 데이터를 가져옴
LIMIT {가져올 갯수} 또는 LIMIT {건너뛸 갯수}, {가져올 갯수}

가져올 갯수가 디폴트 0이라고 생각하면 될듯

~~~Ini
SELECT * FROM Customers
LIMIT 10
~~~
~~~Ini
SELECT * FROM Customers
LIMIT 30, 10
~~~
30개의 열을 건너뛰고 10개를 가져온다


# 연산자
1. 사칙연산

  |연산자|의미|
  |---|---|
  |+, -, \*, / |더하기, 빼기, 곱하기, 나누기|
  |%, MOD|나머지|
  ~~~Ini
  SELECT 5 - 2.5 AS DIFFERENCE;
  ~~~
  연산시 문자열이 있는 경우 0 으로 취급

  ~~~Ini
  SELECT 'ABC' + 3
  result = 3
  ~~~
  문자열 안에 숫자가 있고 숫자랑 연산시 자동으로 숫자로 변환
  ~~~Ini
  SELECT '1' + '002' * 3
  result = 7
  ~~~
  ~~~Ini
  SELECT OrderID,ProductID, 
  OrderID + ProductID AS SumVal

  FROM OrderDetails  ;
  ~~~
  OrderDetails에서 OrderID, ProductID를 불러오고,
  (OrderID+ProductID)한 결과를 SumVal이라는 컬럼으로 가져오겠다

  ~~~Ini
  SELECT
    ProductName,
    Price,
    Price / 2 AS HalfPrice
    Price
  FROM Products;
  ~~~
  Products에서 Price를 가져오고,
  Price 값을 /2해서 HalfPrice로 
  1. 참/거짓 관련 연산자

  |TRUE|FALSE|
  |---|---|
  |1|0|

  ~~~Ini
  SELECT * FROM Customers WHERE FLASE;
  ~~~

  |연산자|의미|
  |---|---|
  |IS| 양쪽 모두 TRUE 또는 FALSE|
  |IS NOT| 양쪽 모두 TRUE 또는 FALSE|

  ~~~Ini
  SELECT (TRUE IS FALSE) IS NOT TRUE;
  ~~~

  |연산자|의미|
  |---|---|
  |AND, &&|양쪽이 모두 TRUE일 때만 TRUE|
  |OR, \|\||한쪽은 TRUE이면 TRUE|

  ~~~Ini
  SELECT * FROM OrderDetails
  WHERE
    ProductId = 20
    AND (OrderId = 10514 OR Quantity = 50);
  ~~~

  OrderDetails 전체 중에서 ProductId 값이 20이고 OrderId = 10514이거나  Quantity = 50 인 데이터를 가져옴



  |연산자|의미|
  |---|---|
  |=|양쪽 값이 같음|
  |!=,<>|양쪽 값이 다름|
  |>,<| (왼쪽, 오른쪽)값이 더 큼|
  |>=, <=| (왼쪽, 오른쪽) 값이 같거나 더 큼|

  ~~~Ini
  SELECT 'A' = 'A', 'A' = 'B', 'A' < 'B', 'A' > 'B';
  ~~~
  문자열에서는 인덱스를 기준으로 크다고 표현한
  즉, A<B 의 결관는 참(1)

  |연산자|의미|
  |---|---|
  |BETWEEN {MIN} AND {MAX}|두 값 사이에 있음|
  |NOT BETWEEN {MIN} AND {MAX}|두 값 사이가 아닌 곳에 있음|

  ~~~Ini
  SELECT 5 BETWEEN 1 AND 10;
  ~~~

  ~~~Ini
  SELECT 'banana' NOT BETWEEN 'Apple' AND 'camera';
  ~~~
  문자열에도 동일하게 적용됨



  ~~~Ini
  SELECT * FROM OrderDetails
  WHERE ProductID BETWEEN 1 AND 4;
  ~~~
  조건문에서 활용가능함


  |연산자|의미|
  |---|---|
  |IN (...)|괄호 안의 값들 중 있음|
  |NOT IN (...)|괄호 안의 값들 중 없음|


  ~~~Ini
  SELECT * FROM Customers
  WHERE City IN ('Torino', 'Paris', 'Portland', 'Madrid') 
  ~~~
  WHERE을 사용해서 열이름을 안에 내용을 선택하여 고를 수 있음


  |연산자|의미|
  |---|---|
  |LIKE '...%...'| 0~N개 문자를 가진 패턴|
  |LIKE '...\_...'| \_갯수만큼의 문자를 가진 패턴| 
  LIKE 연산자는 패턴을 가진 문자열을 찾을때 유용한 연산자

  ~~~Ini
  SELECT * FROM OrderDetails
  WHERE OrderID LIKE '1025_'
  ~~~
  OrderDetails에서 OrderID의 값이 10250번대의 값을 가지는  호출
  ~~~Ini
  SELECT * FROM Customers
  WHERE City Like '%d'
  ~~~
  City의 값이 'd'로 끝나는 데이터 호출



# 함수
1. 숫자와 문자열을 다루는 함수들

  |연산자|의미|
  |---|---|
  |ROUND|반올림|
  |CEIL|올림|
  |FLOOR|내림|
  |ABS|절대값|
  간단해서 패스

  |연산자|의미|
  |---|---|
  |GREATEST|(괄호안에서)가장 큰값|
  |LEAST|(괄호안에서)가장 작은값|

  ~~~Ini
  SELECT
    OrderDetailID, ProductID, Quantity,
    GREATEST(OrderDetailID, ProductID, Quantity),
    LEAST(OrderDetailID, ProductID, Quantity)
  FROM OrderDetails;
  ~~~
  OrderDetails의 (OrderDetailID, ProductID, Quantity)값중 가장 큰것과 작은것을 호출


  |연산자|의미|
  |---|---|
  |MAX|가장 큰 값|
  |MIN|가장 작은값|
  |COUNT|갯수 (NULL은 포함 x)|
  |SUM|총합|
  |AVG|평균 값|

  - GREATEST와 MAX의 차이
    GREATEST와 괄호안의 대상들 사이에서 큰값
    MAX는 열에서 가장 큰값
  ~~~Ini
  SELECT
    MAX(Quantity),
    MIN(Quantity),
    COUNT(Quantity),
    SUM(Quantity),
    AVG(Quantity)
  FROM OrderDetails
  WHERE OrderDetailID BETWEEN 20 AND 30;
  ~~~

  OrderDetailID가 20~30번째 데이터를 가져와서 Quantity열의 데이터를 비교함


  |연산자|의미|
  |---|---|
  |POW(A,B), POWER(A,B)|가장 큰 값|
  |SQRT|제곱근|
  ~~~Ini
  SELECT Price, POW(Price, 1/2)
  FROM Products
  WHERE SQRT(Price) < 4;
  ~~~ 

  Products에서 Price와 Price의 1/2승을 Price의 제곱근 값이 4보다 작으면 가져옴


  |연산자|의미|
  |---|---|
  |TRUMCATE(N,n)|N을 소숫점 n자리까지 선택|
  ~~~Ini
  SELECT
    TRUNCATE(1234.5678, 1),
    TRUNCATE(1234.5678, 2),
    TRUNCATE(1234.5678, 3),
    TRUNCATE(1234.5678, -1),
    TRUNCATE(1234.5678, -2),
    TRUNCATE(1234.5678, -3);
  ~~~
  소숫점에서 짤라내어 데이터를 가져옴



  ~~~Ini
  SELECT Price FROM Products
  WHERE TRUNCATE(Price, 0) = 12;
  ~~~
  Price를 소수점 없이 표현했을대 값이 12와 같으면 데이터를 가져옴

2. 문자와 관련된 함수들

  |연산자|의미|
  |---|---|
  |UCASE, UPPER| 모두 대문자로|
  |LCASE, LOWER| 모두 소문자로|

  ~~~Ini
  SELECT
    UCASE(CustomerName),
    LCASE(ContactName)
  FROM Customers;
  ~~~


   |연산자|의미|
  |---|---|
  |CONCAT(...)|괄호 안의 내용 이어붙임|
  |CONCAT_WS(S, ... )|괄호 안의 내용을 S로 이어붙임|


  ~~~Ini
  SELECT OrderID, CONCAT('O-ID: ', OrderID) FROM Orders;
  ~~~

  ~~~Ini
  SELECT
    FirstName, LastName, CONCAT_WS(' ', FirstName, LastName) AS FullName
  FROM Employees;
  ~~~
  Employees에 FirstName, LastName을 ' '으로 합쳐주어 FUllName이라는 열이름으로 호출



  ~~~Ini
  SELECT OrderID, CONCAT('O-ID: ', OrderID) FROM Orders;
  ~~~


   |연산자|의미|
  |---|---|
  |SUBSTR, SUBSTRING|주어진 값에 따라 문자열을 자름|
  |LEFT|왼쪽부터 N 글자 자름|
  |RIGHT|오른쪽분터 N 글자 자름|

  ~~~Ini
  SELECT
    OrderDate,
    LEFT(OrderDate, 4) AS Year,
    SUBSTR(OrderDate, 6, 2) AS Month,
    RIGHT(OrderDate, 2) AS Day
  FROM Orders;

  ~~~
  1996-07-04와 같은 문자열
  LEFT는 1996을 가져와서 YEAR로 가져옴
  SUBSTR은 앞에서 6번째 문자에서 2개의 문자를 가져와서 MOTH에 저장 
  LIGHT는 04을 가져와서 DAY로 가져옴
  #참고로 SQL문자열은 인덱스가 1부터 시작





