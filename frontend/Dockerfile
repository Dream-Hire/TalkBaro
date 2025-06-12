# 빌드 스테이지
FROM node:20-alpine AS builder
WORKDIR /build

# package.json과 package-lock.json 복사 (의존성 캐싱용)
COPY package*.json ./

# 의존성 설치
RUN npm ci --silent

# 소스 코드 복사
COPY . .

# Vite로 빌드 (정적 파일 생성)
RUN npm run build

# 실행 스테이지 - 정적 파일만 준비
FROM nginx:stable-alpine
COPY --from=builder /build/dist /usr/share/nginx/html

# Nginx 설정 덮어쓰기
COPY ../nginx/default.conf /etc/nginx/conf.d/default.conf

# 포트 노출 (내부적으로만 사용)
EXPOSE 80

# Nginx 실행
CMD ["nginx", "-g", "daemon off;"]