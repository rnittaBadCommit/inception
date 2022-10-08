FROM alpine:3.15

RUN	set -ex; \
	apk update && apk upgrade;

RUN set -ex; \
    apk add nginx openssl; \
    mkdir -p /run/nginx;

# SSL
RUN		mkdir -p /etc/nginx/ssl
WORKDIR	/etc/nginx/ssl/
RUN		openssl req -newkey rsa:4096 \
                -x509 \
                -sha256 \
                -days 3650 \
                -nodes \
                -out ft_server.crt \
                -keyout ft_service.key \
                -subj "/C=JP/ST=Tokyo/L=Shinjukuku/O=University/OU=IT Department/CN=www.example.com";

COPY ./conf/default.conf /etc/nginx/http.d/

RUN		rm -rf /var/cache/apk/*

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
