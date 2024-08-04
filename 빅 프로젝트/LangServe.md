

# requirements.txt
```python
pip install -U langchain-cli pydantic==1.10.13
pip install -U langchain-cli
pip install poetry
pip install langserve

```

# app
```python
langchain app new my-app
langchain app new my-app --package rag-redis
```


# 포트번호 실행
```python
uvicorn server:app --host 0.0.0.0 --port 8080
```



![](https://i.imgur.com/WciaBU7.png)


![](https://i.imgur.com/syILO1Y.png)



# my_app

- RAGPipeLine.py 통째로 넣기

## 결과
- fastapi로는 실행 성공
- langserve 구현 실패
- chain 형태가 아님
- 코드 전체를 뜯어 고쳐서 구조를 바꿔야 할 것 같음




# my_app_2
- prompt 실행해서 playground 작동 확인 하기

## 결과
- playground_type="default" 로 성공
- langserve 잘 작동 함
- playground_type="chat" 으로 해볼 것




# my_app_3
- RAGPipeLine.py 뜯어서 chain 형식으로 만들기

## 결과
- output이 자꾸 쪼개져서 나옴.....

# my_app_4
- RAGPipeLine.py 통째로 넣어서 langserve 사용해보기

## 결과
- output이 잘 들어가는데 출력이 안됨.......





# my_app_redis
- langserve에서 제공하는 redis template 사용

## 결과
- redis 버전이 4.0 이상이 되어야 하는데 git에서 제공해주는 redis 버전이 3.2 까지 밖에 없음.
- template 사용 불가



# my_app_6
- `from langchain_core.output_parsers import StrOutputParser` 사용

## 결과
- 똑같음


# my_app_7 - redis 연결
- RagpipeLine과 redis 연결

## 결과 성공

# my_app_8 - playground, redis 연결
- langserve 연결 확인하기

## 결과
- redis에는 uesremail, session_id 들어감
- 그러나 출력 값은 아직 여전히 안나옴




# my_app_9 
 - 출력값 나타내기