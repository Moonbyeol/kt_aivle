
# 프레임워크

## 비교

| 프레임워크              | HTTP REST 지원 | gRPC 지원   | 지원하는 모델 포맷                                                 | Concurrent Model Execution | Dynamic Batch Inference | 로깅        | 모델 버저닝    | 모델 관리     | 프로메테우스 모니터링 |
| ------------------ | ------------ | --------- | ---------------------------------------------------------- | -------------------------- | ----------------------- | --------- | --------- | --------- | ----------- |
| **FastAPI**        | **O**        | **구현 필요** | **구현 필요**                                                  | **구현 필요**                  | **구현 필요**               | **구현 필요** | **구현 필요** | **구현 필요** | **구현 필요**   |
| Tensorflow Serving | O            | O         | Tensorflow                                                 | X                          | O                       | O         | O         | O         | O           |
| Triton             | O            | O         | Tensorflow, PyTorch, ONNX, TensorRT, OpenVINO, TorchScript | O                          | O                       | O         | O         | O         | O           |
| Django             | O            | 구현 필요     | 구현 필요                                                      | 구현 필요                      | 구현 필요                   | O         | 구현 필요     | 구현 필요     | 구현 필요       |
### 기능 설명

1. **HTTP REST 지원**: HTTP 프로토콜을 통해 RESTful API를 제공하는 기능입니다.
2. **gRPC 지원**: gRPC 프로토콜을 통해 고성능, 다중 언어 지원 API를 제공하는 기능입니다.
3. **지원하는 모델 포맷**: 프레임워크가 직접 지원하는 머신러닝/딥러닝 모델 포맷입니다.
4. **Concurrent Model Execution**: 여러 모델을 동시에 실행할 수 있는 기능입니다.
5. **Dynamic Batch Inference**: 실시간으로 입력 데이터를 묶어(batch) 효율적으로 추론(inference)하는 기능입니다.
6. **로깅**: 시스템 동작 및 오류를 기록하는 기능입니다.
7. **모델 버저닝**: 모델의 버전을 관리하여 여러 버전을 유지하고 사용할 수 있는 기능입니다.
8. **모델 관리**: 모델을 배포, 업그레이드, 모니터링하는 관리 기능입니다.
9. **프로메테우스 모니터링**: Prometheus를 통해 시스템 성능을 모니터링하고 메트릭을 수집하는 기능입니다.

### 프레임워크별 기능 요약

- **FastAPI**: 고성능 비동기 HTTP REST API 프레임워크로, gRPC 지원과 모델 관리 등 고급 기능은 직접 구현이 필요합니다.
- **Tensorflow Serving**: TensorFlow 모델 서빙에 최적화된 프레임워크로, gRPC 지원, 동적 배치 추론, 모델 버저닝 등 고급 기능을 지원합니다.
- **Triton**: 다양한 모델 포맷을 지원하는 강력한 모델 서빙 프레임워크로, 동시 모델 실행, 동적 배치 추론, 모델 관리 등 다양한 고급 기능을 제공합니다.
- **Django**: 강력한 웹 프레임워크로, 기본적인 HTTP REST 지원은 뛰어나지만, gRPC 지원 및 고급 모델 서빙 기능은 직접 구현이 필요합니다.


## FastAPI 선택 이유

1. **비동기 지원**
	- FastAPI는 비동기 코드를 지원하여, 대기 시간(예: 외부 API 호출, 데이터베이스 쿼리 등)을 최소화할 수 있습니다. 이를 통해 응답 속도를 향상시키고 서버 자원을 효율적으로 사용할 수 있습니다. 
	- Django는 기본적으로 동기 처리이며, 비동기 처리를 위해서는 추가 설정이 필요함, Tensorflow Serving 및 Triton은 비동기 처리를 기본적으로 지원하지 않음
    
2. **간편한 사용성 및 높은 생산성**
	- FastAPI는 Python의 타입 힌트를 활용하여 자동으로 API 문서를 생성합니다. 개발자는 Swagger UI 및 ReDoc을 통해 자동 생성된 문서를 쉽게 확인하고 테스트할 수 있습니다. 이는 개발 과정에서 오류를 줄이고, API 개발 시간을 단축시키는 데 크게 기여합니다. 
	- Django의 경우, API 문서 생성을 위해 Django REST Framework와 같은 추가 라이브러리가 필요, Tensorflow Serving 및 Triton은 자동 API 문서 생성 기능이 부족
    
3. **강력한 유효성 검사 및 직관적인 코드**
	- Pydantic을 사용하여 데이터 유효성 검사를 손쉽게 처리할 수 있습니다. FastAPI는 Pydantic 모델을 기반으로 데이터의 유효성을 자동으로 검사하며, 이를 통해 신뢰성 높은 API를 구축할 수 있습니다. 또한, 코드는 직관적이고 읽기 쉬워 유지보수에 용이합니다.
	- Django는 Form 및 ModelForm을 통해 유효성 검사를 지원하지만, FastAPI의 Pydantic과 비교하면 코드의 간결성 및 사용성이 떨어질 수 있음, Tensorflow Serving 및 Triton은 데이터 유효성 검사 기능이 내장되어 있지 않음
    
4. **확장성 및 유연성**
	- FastAPI는 마이크로서비스 아키텍처를 채택하기에 이상적입니다. 각 모듈을 독립적으로 개발하고 확장할 수 있어 큰 프로젝트에서도 효율적으로 작업할 수 있습니다. 또한, SQLAlchemy, Tortoise ORM 등 다양한 데이터베이스 ORM과 쉽게 통합할 수 있어 유연한 개발이 가능합니다.
	- Django는 monolithic architecture를 기본으로 하지만, Django REST Framework를 통해 마이크로서비스 아키텍처를 구현할 수 있음, Tensorflow Serving 및 Triton은 주로 모델 서빙에 집중되어 있어 데이터베이스 ORM과의 통합이 어려움
    
5. **보안 기능 내장**
	- FastAPI는 OAuth2, JWT 등 다양한 인증 및 권한 부여 방식을 기본적으로 지원합니다. 이를 통해 보안이 중요한 애플리케이션에서도 안전하게 사용할 수 있습니다.
	- Django는 기본적으로 강력한 인증 및 권한 부여 시스템을 내장하고 있으며, 다양한 서드 파티 라이브러리를 통해 확장 가능, Tensorflow Serving 및 Triton은 보안 기능이 제한적



# 아키텍처 다이어그램


![](https://i.imgur.com/k08JYNn.png)



# Fastapi

## 가상 환경
### 1. 가상 환경 생성
1) 생성
```python
conda create -n 가상환경명 python=3.11
```
2) 실행
```python
conda activate 가상환경명
```
### 2. requirements
1) requirements.txt 작성
```python
uvicorn
fastapi
sqlalchemy
pymysql
pydantic
pydantic[email]
```
2) requirements.txt  실행
```python
pip install requirements.txt
```

## 아래는 전부 main.py에 작성 
## 라이브러리
```python
from fastapi import FastAPI, Depends, HTTPException
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, Session, declarative_base
from sqlalchemy import Column, Integer, String, ForeignKey, DateTime
from sqlalchemy.sql import func
from sqlalchemy.orm import relationship
from pydantic import BaseModel, EmailStr
from typing import Optional
```


## FastAPI 애플리케이션 생성
```python
# 기본 WAS 설정
# FastAPI 앱을 생성합니다. 이는 웹 애플리케이션 서버를 설정하고 API 엔드포인트를 정의하는 데 사용됩니다.
app = FastAPI()
```

## 데이터베이스
```python
## 데이터베이스 설정
# SQLAlchemy 엔진을 생성하여 MySQL 데이터베이스에 연결합니다.
# `create_engine` 함수는 데이터베이스 URL을 인자로 받아 연결을 설정합니다.
engine = create_engine("mysql+pymysql://사용자:비밀번호@연결주소:3306/db이름")

# 세션 로컬을 설정합니다. 이는 데이터베이스 세션을 관리하기 위해 사용됩니다.
# autocommit=False: 트랜잭션을 수동으로 제어합니다. SQLAlchemy는 기본적으로 자동으로 커밋하지 않으며, 수동으로 커밋하거나 롤백할 수 있습니다.
# autoflush=False: 세션에서 변경된 내용을 자동으로 플러시(디스크로 기록)하지 않습니다. 수동으로 flush를 호출하여 변경 내용을 반영할 수 있습니다.
# bind=engine: 생성된 세션이 위에서 정의한 엔진과 연결되도록 합니다.
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

## 데이터베이스 세션 관리
# 데이터베이스 세션을 가져오는 함수입니다. 요청이 끝나면 세션을 닫습니다.
# `yield`를 사용하여 제너레이터 함수를 정의합니다. 이는 요청마다 새로운 데이터베이스 세션을 생성하고, 요청이 끝나면 세션을 자동으로 종료하는 데 사용됩니다.
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

## 데이터베이스 모델 정의
# `declarative_base`를 사용하여 SQLAlchemy 모델의 기반으로 사용할 기본 클래스(Base)를 생성합니다.
# 이 클래스를 상속하여 데이터베이스 테이블을 정의할 수 있습니다.
Base = declarative_base()

# QnA 테이블을 정의합니다.
# 각 클래스는 데이터베이스 테이블과 매핑되며, 클래스 속성은 테이블의 컬럼과 매핑됩니다.
class QnA(Base):
    __tablename__ = 'qna'
    qna_id = Column(Integer, primary_key=True, index=True)
    email = Column(String(255), ForeignKey('users.email'), nullable=False)
    title = Column(String(255))
    content = Column(String(255))
    created_at = Column(DateTime(timezone=True), server_default=func.now())
    comments = relationship("Comment", back_populates="qna")

# Comment 테이블을 정의합니다.
# 이 클래스는 Comment 테이블과 매핑됩니다.
class Comment(Base):
    __tablename__ = 'comment'
    comment_id = Column(Integer, primary_key=True, index=True)
    qna_id = Column(Integer, ForeignKey('qna.qna_id'), nullable=False)
    email = Column(String(255), ForeignKey('users.email'), nullable=False)
    content = Column(String(255))
    created_at = Column(DateTime(timezone=True), server_default=func.now())
    # QnA와의 관계를 정의합니다.
    qna = relationship("QnA", back_populates="comments")
    # User와의 관계를 정의합니다.
    user = relationship("User", back_populates="comments")
    # Comment와 Image 간의 관계를 정의합니다.
    images = relationship("Image", back_populates="comment")
```


## Pydantic 모델 정의
```python
# 프론트엔드에서 받아올 데이터의 타입을 제약하기 위해 pydantic을 사용합니다.
# Pydantic을 사용하면 데이터 유효성 검사를 자동으로 수행하여, 잘못된 데이터가 들어오는 것을 방지할 수 있습니다.
class QnaCreate(BaseModel):
    email: EmailStr
    title: str
    content: str

class QnaUpdate(BaseModel):
    qna_id: int
    email: EmailStr
    title: str
    content: Optional[str] = None # 빈 값으로도 들어올 수 있음
```


## CRUD(Create,Read,Update,Delete) 함수 정의
```python
# QnA 데이터를 생성하는 함수입니다.
# 데이터베이스 세션을 사용하여 새로운 QnA 데이터를 추가합니다.
def create_qna(db: Session, qna: QnaCreate):
    db_qna = QnA(email=qna.email, title=qna.title, content=qna.content)
    db.add(db_qna)
    db.commit()
    db.refresh(db_qna)
    return db_qna

# 모든 QnA 데이터를 가져오는 함수입니다.
# 데이터베이스 세션을 사용하여 모든 QnA 데이터를 쿼리합니다.
def get_all_qna(db: Session):
    return db.query(QnA).all()

# 특정 QnA 데이터를 가져오는 함수입니다.
# 데이터베이스 세션을 사용하여 특정 QnA 데이터를 쿼리합니다.
def get_qna(db: Session, qna_id: int):
    return db.query(QnA).filter(QnA.qna_id == qna_id).first()

# QnA 데이터를 업데이트하는 함수입니다.
# 데이터베이스 세션을 사용하여 특정 QnA 데이터를 업데이트합니다.
def update_qna(qna: QnaUpdate, db: Session):
    db_qna = db.query(QnA).filter(QnA.qna_id == qna.qna_id).first()
    db_qna.content = qna.content
    db_qna.title = qna.title
    db.commit()
    db.refresh(db_qna)
    return db_qna

# QnA 데이터를 삭제하는 함수입니다.
# 데이터베이스 세션을 사용하여 특정 QnA 데이터를 삭제합니다.
def delete_qna(qna: QnA, db: Session):
    db.delete(qna)
    db.commit()

```


## API 엔드포인트 정의
```python
# 각 CRUD 기능을 제공하는 API 엔드포인트를 정의
# QnA 데이터를 업로드하는 API 엔드포인트입니다.
@app.post("/upload")
async def upload_qna(qna_data: QnaCreate, db: Session = Depends(get_db)):
    # `create_qna` 함수를 호출하여 데이터베이스에 새로운 QnA 데이터를 생성합니다.
    qna = create_qna(db=db, qna=qna_data)
    return qna

# 모든 QnA 데이터를 로드하는 API 엔드포인트입니다.
@app.get("/load_all_qna")
async def load_all_qna(db: Session = Depends(get_db)):
    # `get_all_qna` 함수를 호출하여 모든 QnA 데이터를 가져옵니다.
    return get_all_qna(db)

# 특정 QnA 데이터를 로드하는 API 엔드포인트입니다.
@app.get("/load_qna/{qna_id}")
async def load_qna(qna_id: int, db: Session = Depends(get_db)):
    # `get_qna` 함수를 호출하여 특정 QnA 데이터를 가져옵니다.
    result = get_qna(db, qna_id)
    # 데이터가 없을 경우 404 오류를 발생시킵니다.
    if not result:
        raise HTTPException(status_code=404, detail="QnA not found")
    return result

# QnA 데이터를 업데이트하는 API 엔드포인트입니다.
@app.put("/update_qna")
async def update_qna(qna: QnaUpdate, db: Session = Depends(get_db)):
    # 데이터베이스에서 해당 QnA 데이터를 가져옵니다.
    db_qna = get_qna(db, qna.qna_id)
    # 작성자가 아닌 경우 400 오류를 발생시킵니다.
    if not db_qna or db_qna.email != qna.email:
        raise HTTPException(status_code=400, detail="you are not writer")
    # `update_qna` 함수를 호출하여 QnA 데이터를 업데이트합니다.
    result = update_qna(qna, db)
    return result

# QnA 데이터를 삭제하는 API 엔드포인트입니다.
@app.delete("/delete_qna")
async def delete_qna(qna: QnaUpdate, db: Session = Depends(get_db)):
    # 데이터베이스에서 해당 QnA 데이터를 가져옵니다.
    db_qna = get_qna(db, qna.qna_id)
    # 작성자가 아닌 경우 400 오류를 발생시킵니다.
    if not db_qna or db_qna.email != qna.email:
        raise HTTPException(status_code=400, detail="you are not writer")
    # `delete_qna` 함수를 호출하여 QnA 데이터를 삭제합니다.
    delete_qna(db_qna, db)
    return {"detail": "delete_success"}
```
- **GET**: 데이터를 가져옵니다.
- **POST**: 데이터를 추가합니다.
- **PUT**: 데이터를 수정합니다.
- **DELETE**: 데이터를 삭제합니다.


## 실행
```python
uvicorn main:app --reload 
```


