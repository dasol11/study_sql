# study_sql

<details>
<summary> SELECT 기초 </summary>
<div markdown="1">
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
</div>
</details>


<details>
<summary> 연산자 </summary>
<div markdown="1">
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
</div>
</details>

  
<details>
<summary> 함수 </summary>
<div markdown="1">

# 함수
  <details>
  <summary> 1. 숫자와 문자열을 다루는 함수들</summary>
  <div markdown="1">



  |함수|의미|
  |---|---|
  |ROUND|반올림|
  |CEIL|올림|
  |FLOOR|내림|
  |ABS|절대값|
  간단해서 패스

  |함수|의미|
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


  |함수|의미|
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


  |함수|의미|
  |---|---|
  |POW(A,B), POWER(A,B)|가장 큰 값|
  |SQRT|제곱근|
  ~~~Ini
  SELECT Price, POW(Price, 1/2)
  FROM Products
  WHERE SQRT(Price) < 4;
  ~~~ 

  Products에서 Price와 Price의 1/2승을 Price의 제곱근 값이 4보다 작으면 가져옴


  |함수|의미|
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
  </div>
  </details>

                        
  <details>
  <summary> 2. 문자와 관련된 함수들 </summary>
  <div markdown="1">

  |함수|의미|
  |---|---|
  |UCASE, UPPER| 모두 대문자로|
  |LCASE, LOWER| 모두 소문자로|

  ~~~Ini
  SELECT
    UCASE(CustomerName),
    LCASE(ContactName)
  FROM Customers;
  ~~~


  |함수|의미|
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


  |함수|의미|
  |---|---|
  |SUBSTR, SUBSTRING|주어진 값에 따라 문자열을 자름|
  |LEFT|왼쪽부터 N 글자 자름|
  |RIGHT|오른쪽분터 N 글자 자름|  
  

  

  |함수|의미|
  |---|---|
  |LENGTH|문자열의 바이트 길이|
  |CHAR_LENGTH, CHARACTER_LEGNTH|문자열의 문자 길이|  
  
  
  
    
  |함수|의미|
  |---|---|
  |TRIM|양쪽 공백제거|
  |RTRIM|오른쪽 공백제거|
  |LTRIM|왼쪽 공백제거|  
  
  
  
  
  ~~~Ini
  SELECT
    CONCAT('|', ' HELLO ', '|'),
    CONCAT('|', LTRIM(' HELLO '), '|'),
    CONCAT('|', RTRIM(' HELLO '), '|'),
    CONCAT('|', TRIM(' HELLO '), '|');
  ~~~
  

    
  |함수|의미|
  |---|---|
  |RPAD(S, N, P)|S가 N글자가 될때까지 오른쪽에 P를 이어붙임|
  |LPAD(S, N, P)|S가 N글자가 될때까지 왼쪽에 P를 이어붙임|
  
  
  ~~~Ini
  SELECT
    LPAD(SupplierID, 5, 0),
    RPAD(Price, 6, 0)
  FROM Products;
  ~~~
  
  |함수|의미|
  |---|---|
  |REPLACE(S, A, B)| S중 A를 B로 변경|
  |INSTR(S,s)| S증 s의 첫 위치 반환 , 없으면 0|
  |CAST(A, T)| A를 T자료형으로 변환|

  ~~~Ini
  REPLACE(S, A, B)	
  ~~~
  ~~~Ini
  SELECT
  INSTR('ABCDE', 'ABC'),
  INSTR('ABCDE', 'BCDE'),
  INSTR('ABCDE', 'C'),
  INSTR('ABCDE', 'DE'),
  INSTR('ABCDE', 'F');
  ~~~  
  ~~~Ini
  SELECT
    '01' = '1',
  CONVERT('01', DECIMAL) = CONVERT('1', DECIMAL);
  ~~~
    
  </div>
  </details>
  
  <details>
  <summary> 3. 시간/날짜 관련 및 기타 함수들 </summary>
  <div markdown="1">

  |함수|의미|
  |---|---|
  |CURRENT_DATE, CURDATE| 현재 날짜 반환 |
  |CURRENT_TIME, CURTIME| 현재 시간 반환 |  
  |CURRENT_TIMESTAMP, NOW| 현재 시간과 날짜를 반환|
  
    
  ~~~Ini
  SELECT CURDATE(), CURTIME(), NOW();
  ~~~

  |함수|의미|
  |---|---|
  |DATE| 문자열에 따라 날짜 생성 |
  |TIME| 문자열에 따라 시간 생성 |

  ~~~Ini
  SELECT * FROM Orders
  WHERE
    OrderDate BETWEEN DATE('1997-1-1') AND DATE('1997-1-31');
  ~~~
  1997년 1월 1일 부터 1월 31일 사이의 데이터를 가져옴

  |함수|의미|
  |---|---|
  |YEAR| 주어진 DATETIME값의 년도 반환|
  |MONTHNAME| 주어진 DATETIME값의 월(영문) 반환|
  |MONTH| 주어진 DATETIME값의 월 반환|
  |WEEKDAY| 주어진 DATETIME값의 요일반환 (월요일 : 0)|
  |DAYNAME| 주어진 DATETIME값의 요일명 반환|
  |DAYOFMONTH, DAY| 주어진 DATETIME값의 날짜 반환|
  ~~~Ini
  SELECT * FROM Orders
  WHERE WEEKDAY(OrderDate) = 0;
  ~~~
  OrderDate값의 요일이 월요일(0)이면 불러온다 
  ~~~Ini
  SELECT
  OrderDate,
  CONCAT(
      CONCAT_WS(
        '/',
        YEAR(OrderDate), MONTH(OrderDate), DAY(OrderDate)
      ),
      ' ',
      UPPER(LEFT(DAYNAME(OrderDate), 3))
    )
  FROM Orders;
  ~~~
  OrderDate의 년, 월, 일을 받아와 '/'으로 합쳐주고,
  ' ', DAYNAME(OrderDate)의 왼쪽부터 3번째까지 대문자로 변경한문자열과 합쳐서 반환


  |함수|의미|
  |---|---|
  |HOUR| 주어진 DATETIME의 시 반환|
  |MINUTE| 주어진 DATETIME의 분 반환|
  |SECOND| 주어진 DATETIME의 초 반환|


  ~~~Ini
  SELECT
    HOUR(NOW()), MINUTE(NOW()), SECOND(NOW());
  ~~~
  현재 시간, 분, 초를 반환

  |함수|의미|
  |---|---|
  |ADDDATE, DATE_ADD| 시간/날짜 더하기|
  |SUBDATE, DATE_SUB| 시간 날짜 빼기|
  ~~~Ini
  SELECT 
    ADDDATE('2021-06-20', INTERVAL 1 YEAR),
    ADDDATE('2021-06-20', INTERVAL -2 MONTH),
    ADDDATE('2021-06-20', INTERVAL 3 WEEK),
    ADDDATE('2021-06-20', INTERVAL -4 DAY),
    ADDDATE('2021-06-20', INTERVAL -5 MINUTE),
    ADDDATE('2021-06-20 13:01:12', INTERVAL 6 SECOND);
  ~~~
  INTERVAL을 사용하여 주어진 시간에서 더하기 빼기 가능

  |함수|의미|
  |---|---|
  |ADDDATE, DATE_ADD| 시간/날짜 더하기|
  |SUBDATE, DATE_SUB| 시간 날짜 빼기|


  |함수|의미|
  |---|---|
  |DATE_DIFF| 두 시간/날짜 간 일수차 |
  |TIME_DIFF| 두 시간/날짜 간 시간차|
  |LAST_DAY| 해당 달의 마지막 날짜|

  ~~~Ini
  SELECT
    TIMEDIFF('2021-06-21 15:20:35', '2021-06-21 16:34:41');
  ~~~
  ~~~Ini
  SELECT
    OrderDate,
    LAST_DAY(OrderDate),
    DAY(LAST_DAY(OrderDate)),
    DATEDIFF(LAST_DAY(OrderDate), OrderDate)
  FROM Orders;
  ~~~
  OrderDate,
  OrderDate 달의 마지막 일,
  OrderDate의 주어진 일,
  OrderDate의 마지막 일과 OrderDate의 주어진 일 차이 반환

  |함수|의미|
  |---|---|
  |DATE_FORMAT|시간/날짜를 지정한 형식으로 반환|

  ~~~Ini
  SELECT REPLACE(
    REPLACE(
      DATE_FORMAT(NOW(), '%Y년 %m월 %d일 %p %h시 %i분 %초'),
      'AM', '오전'
    ),
    'PM', '오후'
  )

  ~~~
  현재 시간을 ''안에 지정된 형식으로 반환 후,
  'AM'은 오전,'PM'은 오후로 반환

  |함수|의미|
  |---|---| 
  |STR_TO_DATE(S, F)|S를 F형식으로 해석하여 시간/날짜 생성|


  ~~~Ini
  SELECT
    OrderDate,
    DATEDIFF(
      STR_TO_DATE('1997-01-01 13:24:35', '%Y-%m-%d %T'),
      OrderDate
    ),
    TIMEDIFF(
      STR_TO_DATE('1997-01-01 13:24:35', '%Y-%m-%d %T'),
      STR_TO_DATE(CONCAT(OrderDate, ' ', '00:00:00'), '%Y-%m-%d %T')
    )
  FROM Orders;
  ~~~
  OrderDate의 날짜와 1997년 1월 1일 00시 00분 00초가 얼마나 날짜가 차이나는지 반환
  OrderDate의 시간과 ""의 시간이 얼마나 차이나는지 반환
  OrderDate는 시분초가 없어서 '00:00:00'을 붙혀줌



  </div>
  </details>

                          
  <details>
  <summary> 4. 기타 함수들 </summary>
  <div markdown="1">

  |형식|설명|
  |---|---|    
  | IF(조건, T, F) |조건이 참이면 T, 거짓이면 F반환|
  | IFNULL(A, B) | A가 NULL일 시 B 출력|

  ~~~Ini
  SELECT
    Price,
    IF (Price > 30, 'Expensive', 'Cheap'),
    CASE
      WHEN Price < 20 THEN '저가'
      WHEN Price BETWEEN 20 AND 30 THEN '일반'
      ELSE '고가'
    END
  FROM Products;
  ~~~
  Products 데이터의 Price를 반환,
  Price가 >30이상이면 E, 낮으면 C 반환
  Price 20미만은 저가/ 20이상 30이하는 일반 / 나머지는 고가

  </div>
  </details>

  <details>
  <summary> 5. 조건에 따라 그룹으로 묶기 </summary>
  <div markdown="1">
  
  ## GROUP BY
  GROUP BY : 조건에 따라 **집계된** 값을 가져옴
  (엑셀의 카운트 if와 같은 느낌? 확실 ㄴㄴ)
  ~~~Ini
  
  SELECT CategoryID FROM Products
  GROUP BY CategoryID;
  ~~~
  Products 데이터의 CategoryID 열에 모든 값을 집계해서 CategoryID 그룹으로 묶어서 봄
  
  ### 여러 컬럼을 기준으로 그룹화 가능
  ~~~Ini
  SELECT 
    Country, City,
    CONCAT_WS(', ', City, Country)
  FROM Customers
  GROUP BY Country, City;
  ~~~
  
  |Denmark|Arhus|
  |---|---|
  |Denmark|Kobenhavn|
  Country에서 Denmark안에 Arhus와 Kobenhavn 있는 경우 위 표와 같이 출력됨
  
  ## GROUP BY와 Min, Count()와 같은 함수를 같이 사용
  
  
  ~~~Ini
  SELECT
    CategoryID,
    MAX(Price) AS MaxPrice, 
    MIN(Price) AS MinPrice,
    TRUNCATE((MAX(Price) + MIN(Price)) / 2, 2) AS MedianPrice,
    TRUNCATE(AVG(Price), 2) AS AveragePrice
  FROM Products
  GROUP BY CategoryID;  
    
  ~~~
  Products 테이블을 가져와서 CategoryID로 묶어주고,<br/> 
  CategoryID랑 카테고리 마다의 Price의 최고값, 최소값, 최소최대를 더하고 2로 나눈 것을 소수점 2번째자리까지 표현해서 MedianPrice 열에 불러옴<br/> 
  Price가격의 평균을 구해서 소수점 2번째 자리까지 표현
   
  ~~~Ini
  SELECT
    Country, COUNT(*)
  FROM Suppliers
  GROUP BY Country
  WITH ROLLUP;
  ~~~
  WITH ROLLUP을 추가하면 마지막에 총 몇개인지 테이블에 추가됨,
  즉, 그룹된 값에 대한 합계를 구해줌
  WITH ROLLUP은 ORDER BY와 함께 사용할 수 없음

    
  </div>
  </details>
  
  
  
    
    
  
  
  
  
</div>
</details>
