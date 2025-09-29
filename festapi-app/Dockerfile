#파이썬 이미지 가져오기
FROM python:3.9

#작업 디렉토리 설정
WORKDIR /app

#필요한 파일 복사
COPY . .

#의존성 설치
RUN pip install --no-cache-dir -r requirements.txt

#Fast API 실행
CMD ['uvicorn', 'main:app', '--host', '0.0.0.0', '--port', '8000']