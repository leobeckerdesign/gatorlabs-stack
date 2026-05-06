# Multi-stage build of polotno-puter (the open-source Polotno Studio frontend
# running at studio.polotno.dev). Uses Polotno SDK in demo mode (no commercial
# key required for personal/educational use).
FROM node:20-alpine AS build
WORKDIR /app
RUN apk add --no-cache git python3 make g++ \
 && git clone --depth=1 https://github.com/polotno-project/polotno-puter.git . \
 && npm install --legacy-peer-deps \
 && npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY polotno/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
