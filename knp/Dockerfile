#   Copyright [2018] [Kurohashi-Kawahara lab, Kyoto University]
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

FROM alpine:3.8

ARG KNP_VERSION=4.19
ARG JUMAN_VERSION=7.01

# KNP settings
ARG TARGET=knp
ARG EXTENTION=tar.bz2
ARG URL=http://nlp.ist.i.kyoto-u.ac.jp/nl-resource/${TARGET}/${TARGET}-${KNP_VERSION}.${EXTENTION}
ARG INST_PATH=/usr/local/src/${TARGET}-${KNP_VERSION}.${EXTENTION}
# Juman settings
ARG JUMAN_TARGET=juman
ARG JUMAN_URL=http://nlp.ist.i.kyoto-u.ac.jp/nl-resource/${JUMAN_TARGET}/${JUMAN_TARGET}-${JUMAN_VERSION}.${EXTENTION}
ARG JUMAN_INST_PATH=/usr/local/src/${JUMAN_TARGET}-${JUMAN_VERSION}.${EXTENTION}

WORKDIR /usr/local/src/

# prepare
# after delete
RUN apk update && \
	apk --no-cache --virtual=${TARGET}_rm add \
	curl \
	xz \
	which \
	bzip2 \
	tar \
	gcc \
	g++ \
	make \
	;\
# remains
    apk --no-cache --virtual=${TRAGET} add \
        libstdc++ \
        libgcc \
        boost-dev \
        bash \
        zlib-dev \
	; \
# JUMAN (for juman.h)
    curl -o ${JUMAN_INST_PATH} "${JUMAN_URL}" ;\
    tar jxvf ${JUMAN_TARGET}-${JUMAN_VERSION}.${EXTENTION} ;\
    cd ${JUMAN_TARGET}-${JUMAN_VERSION} ;\
    ./configure ; make ; make install ;\
    cd ../ ; rm -rf ${JUMAN_TARGET}-${JUMAN_VERSION} ;\
    rm -rf ${JUMAN_TARGET}-${JUMAN_VERSION}.${EXTENTION} ;\
# KNP
    curl -o ${INST_PATH} "${URL}" ;\
    tar jxvf ${TARGET}-${KNP_VERSION}.${EXTENTION} ;\
    cd ${TARGET}-${KNP_VERSION} ;\
    ./configure ; make ; make install ;\
    cd ../ ; rm -rf ${TARGET}-${KNP_VERSION} ;\
    rm -rf ${TARGET}-${KNP_VERSION}.${EXTENTION} ;\
    apk del ${TARGET}_rm

CMD ["knp"]

