FROM --platform=${TARGETPLATFORM} liferay/base:latest

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --yes build-essential ca-certificates curl libcups2-dev libfontconfig1-dev libfreetype6-dev libgif-dev libjpeg-dev libltdl-dev liblzma-dev libpng-dev libtiff-dev libwebp-dev libx11-dev libxext-dev libxml2-dev zlib1g-dev && \
	mkdir /build

RUN curl -L -o /build/ghostscript.tar.gz https://github.com/ArtifexSoftware/ghostpdl-downloads/releases/download/gs10040/ghostscript-10.04.0.tar.gz && \
	cd /build && \
	tar -xvzf ghostscript.tar.gz && \
	cd ghostscript-* && \
	./configure --prefix=/usr/local && \
	make && \
	make install && \
	rm -rf /build/*

RUN curl -L -o /build/ImageMagick.tar.gz https://download.imagemagick.org/ImageMagick/download/releases/ImageMagick-7.1.1-43.tar.gz && \
    cd /build && \
    tar -xvzf ImageMagick.tar.gz && \
    cd ImageMagick-* && \
    ./configure --prefix=/usr/local && \
    make && \
    make install && \
    ldconfig /usr/local/lib && \
    rm -rf /build/*
	
RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --no-install-recommends --yes bc ffmpeg file fonts-dejavu google-perftools gifsicle libtcnative-1 && \
	apt-get upgrade --yes && \
	apt-get clean


ARG LABEL_BUILD_DATE
ARG LABEL_NAME
ARG LABEL_VCS_REF
ARG LABEL_VCS_URL
ARG LABEL_VERSION
ARG TARGETPLATFORM

ENV LANG="C.UTF-8"

LABEL org.label-schema.build-date="${LABEL_BUILD_DATE}"
LABEL org.label-schema.name="${LABEL_NAME}"
LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.vcs-ref="${LABEL_VCS_REF}"
LABEL org.label-schema.vcs-url="${LABEL_VCS_URL}"
LABEL org.label-schema.vendor="Liferay, Inc."
LABEL org.label-schema.version="${LABEL_VERSION}"