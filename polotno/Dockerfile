# Multi-stage build of polotno-demo (the official minimal Polotno SDK example,
# at github.com/polotno-project/polotno-site/tree/source/examples/polotno-demo).
# No Puter dependency - pure React + Polotno SDK in demo mode.
# Built in CI, served via nginx as a static SPA.
FROM node:20-alpine AS build
WORKDIR /app
RUN apk add --no-cache git python3 make g++ \
 && git clone --depth=1 --filter=blob:none --no-checkout --branch source \
      https://github.com/polotno-project/polotno-site.git /tmp/site \
 && cd /tmp/site \
 && git sparse-checkout init --cone \
 && git sparse-checkout set examples/polotno-demo \
 && git checkout source \
 && cp -r /tmp/site/examples/polotno-demo/. /app/ \
 && rm -rf /tmp/site \
 && npm install --legacy-peer-deps \
 && CI=false npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY polotno/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
HEALTHCHECK --interval=30s --timeout=5s --retries=3 --start-period=15s \
  CMD wget -q -O - http://127.0.0.1/healthz || exit 1
CMD ["nginx","-g","daemon off;"]
