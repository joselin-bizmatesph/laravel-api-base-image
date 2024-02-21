#FROM nginx:alpine
FROM public.ecr.aws/docker/library/nginx:1.23.1-alpine

ENV APP_ENV="prod"
ARG APP_ENV

WORKDIR '/laravel-project'

RUN apk --no-cache add shadow

COPY ["./","./"]
COPY ["./docker/${APP_ENV}/nginx/nginx.conf", "/etc/nginx/nginx.conf"]
COPY ["./docker/${APP_ENV}/nginx/docker-entrypoint.sh", "/docker-entrypoint.sh"]
RUN chmod +x /docker-entrypoint.sh

EXPOSE 80

ENTRYPOINT ["/docker-entrypoint.sh"]
