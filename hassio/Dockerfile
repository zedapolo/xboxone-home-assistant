ARG BUILD_FROM
FROM $BUILD_FROM

ENV LANG C.UTF-8

# Install requirements for add-on
RUN apk add --no-cache \
	 jq \
	 python3 \
	 libffi \
	 openssl \
      && apk add --no-cache --virtual .build-dependencies \
	 gcc \
         musl-dev \
	 python3-dev \
	 libffi-dev \
         openssl-dev \
      && python3 -m ensurepip \
      && rm -r /usr/lib/python*/ensurepip \
      && pip3 install --upgrade pip setuptools \
      && if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi \
      && if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi \
      && rm -r /root/.cache

RUN pip3 install xbox-smartglass-core==1.1.2

COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
