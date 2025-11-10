# Python 3.9 베이스 이미지 사용
FROM python:3.9-slim AS base

# 작업 디렉토리 설정
WORKDIR /app

# 의존성 파일만 먼저 복사
COPY requirements.txt .

# 의존성 설치
RUN pip install --no-cache-dir -r requirements.txt
ENV PATH="/home/appuser/.local/bin:$PATH"

# 필요한 파일 복사
COPY main.py .
COPY templates/ ./templates/
COPY todo.json .

# FastAPI 서버 실행 poetry run 
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]