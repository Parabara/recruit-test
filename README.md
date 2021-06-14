## 파라바라 Mobile 사전과제
### BaseURL : https://api.recruit-test.parabara.kr

### 이미지 업로드

URI : POST /api/product/upload

##### Request Param

|Key|Description|Type|Required|
|------|---|---|---|
|image|Multipart File|File|Y|

```
curl \
-H 'x-token: 123456' \
-X POST -F 'image=@/Users/yeonjung/Desktop/image.png' \
https://api.recruit-test.parabara.kr/api/product/upload
```

##### Response

|Key|Description|Type|Required|
|------|---|---|---|
|id|이미지 아이디|Long|Y|
|url|이미지 경로|String|Y|

```
{
    "code": "200",
    "status": 200,
    "data": {
        "id": 16,
        "url": "https://d2jtcj253cfxcl.cloudfront.net/test/202106/95772c00-a70f-4a80-8dd4-e21c51c0abdf.jpg"
    },
    "error": false,
    "message": "SUCCESS"
}
```

### 상품 등록 

URI : POST /api/product

##### Request Param

|Key|Description|Type|Required|
|------|---|---|---|
|title|상품 제목|String|Y|
|content|상품 내용|String|Y|
|price|상품 가격|Long|Y|
|images|상품 이미지 아이디 목록|Array< Long >|N|

```
curl \
-H "x-token: 123456" \
-X POST \
-F title=title \
-F content=content \
-F price=10000 \
-F images=1 \
-F images=2 \
https://api.recruit-test.parabara.kr/api/product
```

##### Response

|Key|Description|Type|Required|
|------|---|---|---|
|id|상품 아이디|Long|Y|
|title|상품 제목|String|Y|
|content|상품 내용|String|Y|
|price|상품 가격|Long|Y|
|images|상품 이미지 목록|Array< String >|Y|

```
{
    "code": "200",
    "status": 200,
    "data": {
        "id": 20,
        "title": "asdfas12121231",
        "content": "dsafsadf213123",
        "price": 1000,
        "images": [
            "https://d2jtcj253cfxcl.cloudfront.net/test/202106/49ee3231-1181-4f7b-a170-22f987f48cdb.jpg",
            "https://d2jtcj253cfxcl.cloudfront.net/test/202106/930ef147-72b3-4870-81b1-96fb5b561f54.jpg"
        ]
    },
    "error": false,
    "message": "SUCCESS"
}
```

### 상품 업데이트

URI : PUT /api/product

##### Request Param

|Key|Description|Type|Required|
|------|---|---|---|
|id|상품 아이디|Long|Y|
|title|상품 제목|String|Y|
|content|상품 내용|String|Y|
|price|상품 가격|Long|Y|

```
curl \
-H "x-token: 123456" \
-X PUT \
-F id=1 \
-F title=title \
-F content=content \
-F price=10000 \
https://api.recruit-test.parabara.kr/api/product
```

##### Response
|Key|Description|Type|Required|
|------|---|---|---|
|id|상품 아이디|Long|Y|
|title|상품 제목|String|Y|
|content|상품 내용|String|Y|
|price|상품 가격|Long|Y|
|images|상품 이미지 목록|Array< String >|Y|
```
{
    "code": "200",
    "status": 200,
    "data": {
        "id": 20,
        "title": "asdfas12121231",
        "content": "dsafsadf213123",
        "price": 1000,
        "images": [
            "https://d2jtcj253cfxcl.cloudfront.net/test/202106/49ee3231-1181-4f7b-a170-22f987f48cdb.jpg",
            "https://d2jtcj253cfxcl.cloudfront.net/test/202106/930ef147-72b3-4870-81b1-96fb5b561f54.jpg"
        ]
    },
    "error": false,
    "message": "SUCCESS"
}
```
#### 상품 삭제 
URI : DELETE /api/product/{id}

##### Request Path
|Key|Description|Type|Required|
|------|---|---|---|
|id|상품 아이디|Long|Y|

```
curl \
-H "x-token: 123456" \
-X DELETE \
https://api.recruit-test.parabara.kr/api/product/{id}
```

##### Response
|Key|Description|Type|Required|
|------|---|---|---|
|data|성공여부|Boolean|Y|
```
{
    "code": "200",
    "status": 200,
    "data": true,
    "error": false,
    "message": "SUCCESS"
}
```

#### 상품 리스트 조회
URI : GET /api/product

##### Request Param
|Key|Description|Type|Required|
|------|---|---|---|
|page|현재페이지|Integer|Y|
|size|페이징사이즈|Integer|Y|

```
curl \
-H "x-token: 123456" \
-X GET \
-F page=1 \
-F size=10 \
https://api.recruit-test.parabara.kr/api/product
```

##### Response
|Key|Description|Type|Required|
|------|---|---|---|
|page|현재페이지|Integer|Y|
|total|총 페이지 수|Integer|Y|
|records|총 레코드 수|Integer|Y|
|rows|상품정목 목록|Array< Object >|Y|

##### rows
|Key|Description|Type|Required|
|------|---|---|---|
|id|상품 아이디|Long|Y|
|title|상품 제목|String|Y|
|content|상품 내용|String|Y|
|price|상품 가격|Long|Y|
|images|상품 이미지 목록|Array< String >|Y|
```
{
    "code": "200",
    "status": 200,
    "data": {
        "page": 1,
        "total": 1,
        "records": 19,
        "rows": [
            {
                "id": 21,
                "title": "title",
                "content": "content",
                "price": 10000,
                "images": [
                    "https://d2jtcj253cfxcl.cloudfront.net/test/202106/49ee3231-1181-4f7b-a170-22f987f48cdb.jpg",
                    "https://d2jtcj253cfxcl.cloudfront.net/test/202106/930ef147-72b3-4870-81b1-96fb5b561f54.jpg"
                ]
            } ...n
        ]
    },
    "error": false,
    "message": "SUCCESS"
}
```

#### 상품 상세 조회
URI : GET /api/product/{id}

##### Request Path
|Key|Description|Type|Required|
|------|---|---|---|
|id|상품 아이디|Long|Y|

```
curl \
-H "x-token: 123456" \
-X GET \
https://api.recruit-test.parabara.kr/api/product/{id}
```

##### Response

|Key|Description|Type|Required|
|------|---|---|---|
|id|상품 아이디|Long|Y|
|title|상품 제목|String|Y|
|content|상품 내용|String|Y|
|price|상품 가격|Long|Y|
|images|상품 이미지 목록|Array< String >|Y|

```
{
    "code": "200",
    "status": 200,
    "data": {
        "id": 20,
        "title": "asdfas12121231",
        "content": "dsafsadf213123",
        "price": 1000,
        "images": [
            "https://d2jtcj253cfxcl.cloudfront.net/test/202106/49ee3231-1181-4f7b-a170-22f987f48cdb.jpg",
            "https://d2jtcj253cfxcl.cloudfront.net/test/202106/930ef147-72b3-4870-81b1-96fb5b561f54.jpg"
        ]
    },
    "error": false,
    "message": "SUCCESS"
}
```

#===========================
### Request Header
|x-token|Description| 
|------|---|
|토큰값|사용자별로 부여된 토큰값|

### Response
#### data
|data|Description| 
|------|---|
|Response Data|Response Data|


#### status
|status|Description| 
|------|---|
|200|성공|
|403|권한없음|
|500|Server Error|

#### message
|message|Description| 
|------|---|
|SUCCESS|성공|
|실패메시지|실패메시지|

#### error
|error|Description| 
|------|---|
|false|성공|
|true|실패|

```
{
    "code": "403",
    "status": 403,
    "data": null,
    "error": true,
    "message": "권한이 없습니다."
}
```