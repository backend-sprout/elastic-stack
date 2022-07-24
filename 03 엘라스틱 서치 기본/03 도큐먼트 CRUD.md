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
* `index2` : 인덱스 이름
* `_doc` : 엔드포인트 구분을 위한 예약어
* `1` : 인덱싱할 도큐먼트의 고유 아이디    
  
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

```
GET index2
```
```
{
  "index2": {
    "aliases": {},
    "mappings": {
      "properties": {
        "age": {
          "type": "long"
        },
        "gemder": {
          "type": "text",
          "fields": {
            "keyword": {
              "type": "keyword",
              "ignore_above": 256
            }
          }
        },
        "name": {
          "type": "text",
          "fields": {
            "keyword": {
              "type": "keyword",
              "ignore_above": 256
            }
          }
        }
      }
    },
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "1",
        "provided_name": "index2",
        "creation_date": "1658673645752",
        "number_of_replicas": "1",
        "uuid": "39edIHWiQNy4xZSYfpgSAA",
        "version": {
          "created": "8030299"
        }
      }
    }
  }
}
```
우리가 데이터 타입을 지정하지 않아도,   
엘라스틱서치는 도큐먼트의 필드와 값을 보고 자동으로 지정한다.   
이런 기능을 **다이나믹 매핑**이라고 한다. 

참고로 숫자를 문자열로 입력해도 숫자로 변환시키고, 소수점은 정수로 바꾼다.   

## 도큐먼트 읽기 

도큐먼트를 읽는 방법은 크게 2가지이다.  

1. 도큐먼트 아이디를 통해 조회
2. DSL 쿼리문 

**도큐먼트 아이디를 통해 조회**   
```
GET index2/_doc/1

-----

{
  "_index": "index2",
  "_id": "1",
  "_version": 1,
  "_seq_no": 0,
  "_primary_term": 1,
  "found": true,
  "_source": {
    "name": "mike",
    "age": 25,
    "gemder": "male"
  }
}
```
* 인덱스명과 도큐먼트 아이디를 이용해 특정 도큐먼트의 데이터를 가져올 수 있다.   
* 하지만, 실제 빅데이터에서는 도큐먼트를 하나씩 읽어오는 경우는 드물다.  

**DSL 쿼리문**
```
GET index2/_search
```
* search 라는 DSL쿼리를 사용하면, index2 인덱스 내의 모든 도큐먼트를 가져온다. 

## 도큐먼트 수정 

```
PUT index2/_doc/1
{
  "name": "park",
  "age" : 45,
  "gender" : "male"
}
```
```
{
  "_index": "index2",
  "_id": "1",
  "_version": 2,
  "result": "updated",
  "_shards": {
    "total": 2,
    "successful": 1,
    "failed": 0
  },
  "_seq_no": 3,
  "_primary_term": 1
}
```
결과를 보며느 result에 업데이트가 되었다고 알려준다.   

```
POST index2/_update/1
{
  "doc": {
    "name" : "lee"
  }
}
```
* REST API를 이용해서 특정 도큐먼트의 값을 업데이트할 수도 있다.   
* `_update`라는 엔드포인트를 추가해 특정 필드의 값만 업데이트한 것이  
 
엘라싁서치에서의 도큐먼트 수정 작업은 비용이 많이 들기 때문에 권장하지는 않는다.      
특히 엘라스틱서치를 로그 수집 용도로 사용한다면 개별 도큐먼트를 수정할 일은 거의 없다.  
개별 도큐먼트 수정 작업이 많은 작업이라면 엘라스틱서치보다 다른 벤터를 이용하는 것이 좋다.  

## 도큐먼트 삭제 

도큐먼트를 삭제하기 위해서는 인덱스명과 도큐먼트 아이디를 알고 있어야한다.   


```
DELETE idnex2/_doc/2
```  

도큐먼트를 수정과 마찬가지로 개별 도큐먼트 삭제 또한 비용이 많이 들어가는 작업이니 주의하자.  
