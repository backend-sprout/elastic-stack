# 도큐먼트 CRUD
## 인덱스 생성/확인/삭제

```
PUT(POST) 인덱스이름
GET 인덱스이름
DELETE 인덱스이름
```

* PUT : 생성 혹은 수정
* POST : 생성
* GET : 조회
* DELETE : 삭제

## 도큐먼트 생성

도큐먼트는 반드시 하나의 인덱스에 포함되어야한다.    
엘라스틱서치에서 도큐먼트를 인덷ㄱ스에 포함시키는 것을 인덱싱이라고 한다.  

**실행**
```
PUT index2/_doc/1
{
  "name" : "mike",
  "age" : 25,
  "gemder" : "male"
}
```  
  
**결과**
```
{
  "_index": "index2",
  "_id": "1",
  "_version": 1,
  "result": "created",
  "_shards": {
    "total": 2,
    "successful": 1,
    "failed": 0
  },
  "_seq_no": 0,
  "_primary_term": 1
}
```

index2 인덱스를 생성하면서 동시에 도큐먼트를 인덱싱한다.   
