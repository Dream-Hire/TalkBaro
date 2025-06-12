# 빌드 스테이지
FROM node:20-alpine AS builder
WORKDIR /build

# package.json과 package-lock.json 복사 (의존성 캐싱용)
COPY package*.json ./

# 의존성 설치
RUN npm ci --only=production --silent

# 소스 코드 복사
COPY . .

# Vite로 빌드 (정적 파일 생성)
RUN npm run build

# 실행 스테이지 - 정적 파일만 준비
FROM alpine:latest
COPY --from=builder /build/dist /build/dist

# 외부에서 접근 가능한 볼륨으로 지정
VOLUME ["/build/dist"]

# 컨테이너가 종료되지 않도록 대기
CMD ["tail", "-f", "/dev/null"]