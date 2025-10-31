# Python 3.9 베이스 이미지 사용
FROM python:3.9-slim AS base

# 시스템 패키지 업데이트
RUN apt-get update && apt-get install -y --no-install-recommends \
    libglib2.0-0 libgl1 curl \
 && rm -rf /var/lib/apt/lists/*

# 애플리케이션 용 사용자 생성
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser

# 작업 디렉토리 설정
WORKDIR /app

# 의존성 파일만 먼저 복사
COPY --chown=appuser:appgroup --chmod=644 requirements.txt .

# 의존성 설치
RUN pip install --no-cache-dir --user -r requirements.txt

# 필요한 파일 복사
COPY --chown=appuser:appgroup --chmod=755 . .

USER appuser

ENV PATH="/home/appuser/.local/bin:${PATH}"
EXPOSE 8000

# FastAPI 서버 실행
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]