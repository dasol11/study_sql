# study_sql


FROM : 특정 테이블을 호출하는 함수
SELECT : 특정 컬럼을 가져오겠다
- AS : 특정 컬럼의 이름을 변경하여 호출
 
## EX)
'''Ini
SELECT * FROM Customers
'''
## EX2)
SELECT
  CustomerId AS ID,
  CustomerName AS "이름",
  Address AS ADDR
FROM Customers
한글은 "문자열"

WHERE  : 구문 뒤에 조건을 붙여 원하는 데이터만 가져옴

## EX)
SELECT * FROM Orders
WHERE EmployeeID = 3;


ORDER BY : 특정 구문을 사용해서 특정 컬럼을 기준으로 데이터를 정렬
- ASC : 오름차순
- DESC : 내림차순


# EX)
SELECT * FROM OrderDetails
ORDER BY ProductID ASC, Quantity DESC
먼저 ProductID를 오름차순으로 정렬 후,
ProductID가 같은 행에서는 Quantity는 내림차순으로 정렬

LIMIT : 원하는 만큼만 데이터를 가져옴
LIMIT {가져올 갯수} 또는 LIMIT {건너뛸 갯수}, {가져올 갯수}

가져올 갯수가 디폴트 0이라고 생각하면 될듯

# EX)
SELECT * FROM Customers
LIMIT 10
# EX2)
SELECT * FROM Customers
LIMIT 30, 10
- 30개의 열을 건너뛰고 10개를 가져온다


# 연산자
# 1. 사칙연산
Ex)
SELECT 5 - 2.5 AS DIFFERENCE;

연산시 문자열이 있는 경우 0 으로 취급

# EX)
SELECT 'ABC' + 3
result = 3
- 문자열 안에 숫자가 있고 숫자랑 연산시 자동으로 숫자로 변환
# EX)
SELECT '1' + '002' * 3
result = 7




