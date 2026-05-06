# Multi-stage: extract Garage binary into Alpine so we have a shell
# (dxflrs/garage is distroless — no /bin/sh, no base64).
# Compose passes the TOML via GARAGE_CONFIG_B64 env var; entrypoint decodes it.
FROM dxflrs/garage:v2.3.0 AS source

FROM alpine:3.20
RUN apk add --no-cache ca-certificates tini coreutils
COPY --from=source /garage /usr/local/bin/garage
RUN mkdir -p /var/lib/garage/meta /var/lib/garage/data /etc/garage

EXPOSE 3900 3901 3903

ENTRYPOINT ["/sbin/tini","--"]
CMD ["sh","-c","echo $GARAGE_CONFIG_B64 | base64 -d > /etc/garage.toml && exec /usr/local/bin/garage server"]
