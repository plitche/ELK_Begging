# ELK_Beginning

### Command List
  1. curl https://localhost:9200 -u elastic:password -k
  2. 


### Query DSL
  
##### Full Text Search
- json 형식의 쿼리를 사용  
- 기본 문법
  > GET index/_search
  1. match_all: 별다른 조건 없이 해당 인덱스의 모든 도큐먼트를 검색(생략 가능)
    ```json
      {
        "query":{
          "match_all":{ }
        }
      }
    ```

  2. match: 특정 필드에 원하는 text가 포함되어 있는 모든 문서 검색
    ```json
      {
        "query": {
          "match": {
            "field": "text"
          }
        }
      }
    ```
    2-1. OR 조건
      ```json
        {
          "query": {
            "match": {
              "field": "text1 text2"
            }
          }
        }
      ```
    2-2. AND 조건
      ```json
      {
        "query": {
          "match": {
            "field": {
              "query": "text1 text2",
              "operator": "and"
            }
          }
        }
      }
      ```
  3. match_phrase: "text1 text2"라는 단어의 공백을 포함한 일치하는 도큐먼트를 검색하기 위한 방법. 검색어 순서까지 고려한다. slop은 사이에 다른 단어가 끼어드는 것을 허용하는 단어 개수
    ```json
    {
      "query": {
        "match_phrase": {
          "field": "text1 text2",
          "slop": 1
        }
      }
    }
    ```
  4. query_string: URL검색의 루씬 검색 문법을 이용하고 싶을 때 사용. ("text1"과 "text2"를 모두 포함하거나 또는 "text3 text4"를 포함하는 도큐먼트 검색)
    ```json
    {
      "query": {
        "query_string": {
          "default_field": "field",
          "query": "(text1 AND text2) OR \"text3 text4\""
        }
      }
    }
    ```
  
