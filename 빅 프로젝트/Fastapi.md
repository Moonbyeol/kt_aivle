
# 1. 설치
```
pip install "fastapi[all]" # fastapi 설치 
pip install "uvicorn[standard]" # uvicorn 설치
pip install sqlalchemy # SQLAlchemy 설치
pip install python-multipart
pip install "python-jose[cryptography]"
pip install alembic

```


![](https://i.imgur.com/DgeX2CX.png)


```
alembic init migrations # alembic 초기화

uvicorn main:app --relaod --port 8000 # 실행

```


