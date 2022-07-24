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




 "_source": {***
  "_source": {ㅎㅏㄴ다. 
  "_source": { 
  
  
