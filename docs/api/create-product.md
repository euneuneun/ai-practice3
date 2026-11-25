# 상품 등록

domain: product

url: /api/products

method: POST

success: `201 Created`

# 01. 설명

새 상품을 등록할 때 사용한다.

- 필수: name, price, stock
- 선택: 없음
- 필드 구성 결정 필요 D1, 상품명 규칙 결정 필요 D2, 가격 규칙 결정 필요 D3, 인증·권한 결정 필요 D4, 상품명 중복 처리 결정 필요 D5, 카테고리·이미지·설명 등 추가 필드 결정 필요 D6, 등록자 기록 결정 필요 D7, 등록 후 응답 내용 결정 필요 D8

# 02. 요청(Request)

## a. Parameter & Querystring

```txt
/api/products
```

| 이름 | 데이터타입 | 필수 | 설명 |
|---|---|---|---|
| 없음 | | | |

## b. request headers

| 이름 | 데이터타입 | 필수 | 설명 |
|---|---|---|---|
| Content-Type | String | Y | `application/json` |

인증 헤더 필요 여부는 결정 필요 D4.

## c. request body

```json
{
  "name": "무선 마우스",
  "price": 25000,
  "stock": 100
}
```

| 이름 | 데이터타입 | 필수 | 설명 |
|---|---|---|---|
| name | String | Y | 상품명. 길이 결정 필요 D2 |
| price | Long | Y | 가격(원). 범위 결정 필요 D3 |
| stock | Integer | Y | 재고 수량. 포함 여부·범위 결정 필요 D1 |

# 03. 응답(Response)

## a. response header

| 이름 | 데이터타입 | 필수 | 설명 |
|---|---|---|---|
| Content-Type | String | Y | `application/json` |

## b. response body

**성공 응답:** `201 Created`

```json
{
  "id": 1,
  "name": "무선 마우스",
  "price": 25000,
  "stock": 100,
  "createdAt": "2026-11-25T10:00:00"
}
```

| 이름 | 데이터타입 | 필수 | 설명 |
|---|---|---|---|
| id | Long | Y | 생성된 상품 식별자 |
| name | String | Y | 상품명 |
| price | Long | Y | 가격(원) |
| stock | Integer | Y | 재고 수량 |
| createdAt | String | Y | 등록 일시 |

**에러 응답:** `400 Bad Request` — 필수 값이 없거나 형식이 올바르지 않을 때

```json
{
  "status": 400,
  "message": "요청 값이 올바르지 않습니다."
}
```

| 이름 | 데이터타입 | 필수 | 설명 |
|---|---|---|---|
| status | Integer | Y | HTTP 상태 코드 |
| message | String | Y | 에러 메시지 |

**에러 응답:** `400 Bad Request` — 가격 또는 재고가 허용 범위를 벗어났을 때 (범위 결정 필요 D1, D3)

```json
{
  "status": 400,
  "message": "가격 또는 재고가 올바르지 않습니다."
}
```

| 이름 | 데이터타입 | 필수 | 설명 |
|---|---|---|---|
| status | Integer | Y | HTTP 상태 코드 |
| message | String | Y | 에러 메시지 |
