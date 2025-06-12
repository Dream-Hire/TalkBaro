# 빌드 스테이지
FROM node:20-alpine AS builder
WORKDIR /build

# package.json과 package-lock.json 복사 (의존성 캐싱용)
COPY frontend/package*.json ./

# 의존성 설치
RUN npm ci --only=production --silent

# 소스 코드 복사
COPY frontend/. .

# Vite로 빌드 (정적 파일 생성)
RUN npm run build