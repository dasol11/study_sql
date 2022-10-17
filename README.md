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
|OR,| |한쪽은 TRUE이면 TRUE|
