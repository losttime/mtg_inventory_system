FROM python:3.11.5-alpine3.18 as mtg-inventory

# the image this creates started with python and added postgresql14-client
# 
# from dockerfile for postgres on alpine 3.18, found here:
# https://github.com/docker-library/postgres/blob/05f691067b29d8fb4211a47da37a381d58d36691/14/alpine3.18/Dockerfile

# 70 is the standard uid/gid for "postgres" in Alpine
# https://git.alpinelinux.org/aports/tree/main/postgresql/postgresql.pre-install?h=3.12-stable
# RUN set -eux; \
# 	addgroup -g 70 -S postgres; \
# 	adduser -u 70 -S -D -G postgres -H -h /var/lib/postgresql -s /bin/sh postgres; \
# 	mkdir -p /var/lib/postgresql; \
# 	chown -R postgres:postgres /var/lib/postgresql

# make the "en_US.UTF-8" locale so postgres will be utf-8 enabled by default
# alpine doesn't require explicit locale-file generation
ENV LANG en_US.utf8

RUN set -eux; \
        apk add --no-cache --virtual .build-deps \
        postgresql14-client \
        coreutils \
		dpkg-dev dpkg \
		flex \
		g++ \
		gcc \
		krb5-dev \
		libc-dev \
		libedit-dev \
		libxml2-dev \
		libxslt-dev \
		linux-headers \
		make \
		openldap-dev \
		openssl-dev \
		perl-dev \
		perl-ipc-run \
		perl-utils \
		tcl-dev \
		util-linux-dev \
		zlib-dev \
        bash \
		su-exec \
		tzdata \
		zstd \
	;

WORKDIR /src

RUN pip install --upgrade pip
COPY ./requirements/inventory_requirements.txt requirements.txt
RUN pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
