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
|LIKE '..._...'| _갯수만큼의 문자를 가진 패턴| 
LKIKE 연산자는 패턴을 가진 문자열을 찾을때 유용한 연산자

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



