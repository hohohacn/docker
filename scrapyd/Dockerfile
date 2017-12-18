#
# Dockerfile for scrapyd
#
FROM debian:jessie
MAINTAINER Alex <2314203594@qq.com>

RUN set -xe \
    && apt-get update \
    && apt-get install -y autoconf \
                          build-essential \
                          curl \
                          git \
                          libffi-dev \
                          libssl-dev \
                          libtool \
 			  libmysqlclient-dev \
                          libxml2 \
                          libxml2-dev \
                          libxslt1.1 \
                          libxslt1-dev \
                          python \
                          python-dev \
                          vim-tiny \
			  python-mysqldb \
    && apt-get install -y libtiff5 \
                          libtiff5-dev \
                          libfreetype6-dev \
                          libjpeg62-turbo \
                          libjpeg62-turbo-dev \
                          liblcms2-2 \
                          liblcms2-dev \
                          libwebp5 \
                          libwebp-dev \
                          zlib1g \
                          zlib1g-dev \
			  libmysqlclient-dev \
    && curl -sSL https://bootstrap.pypa.io/get-pip.py | python \
    && pip install git+https://github.com/scrapy/scrapy.git \
                   git+https://github.com/scrapy/scrapyd.git \
                   git+https://github.com/scrapy/scrapyd-client.git \
                   git+https://github.com/scrapinghub/scrapy-splash.git \
                   git+https://github.com/scrapinghub/scrapyrt.git \
                   git+https://github.com/python-pillow/Pillow.git \
		   mysqlclient \
		   SQLAlchemy \
		   cron \
		   lxml \
    && curl -sSL https://github.com/scrapy/scrapy/raw/master/extras/scrapy_bash_completion -o /etc/bash_completion.d/scrapy_bash_completion \
    && echo 'source /etc/bash_completion.d/scrapy_bash_completion' >> /root/.bashrc \
    && apt-get purge -y --auto-remove autoconf \
                                      build-essential \
                                      libffi-dev \
                                      libssl-dev \
                                      libtool \
                                      libxml2-dev \
                                      libxslt1-dev \
                                      python-dev \
    && apt-get purge -y --auto-remove libtiff5-dev \
                                      libfreetype6-dev \
                                      libjpeg62-turbo-dev \
                                      liblcms2-dev \
                                      libwebp-dev \
                                      zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

COPY ./scrapyd.conf /etc/scrapyd/
COPY requirements.txt /stack-requirements.txt
RUN pip install --no-cache-dir -r stack-requirements.txt
VOLUME /etc/scrapyd/ /var/lib/scrapyd/
EXPOSE 6800

CMD ["scrapyd", "--pidfile="]
