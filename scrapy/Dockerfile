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
			  cron \
    && curl -sSL https://bootstrap.pypa.io/get-pip.py | python \
    && pip install git+https://github.com/scrapy/scrapy.git \
		   mysqlclient \
		   SQLAlchemy \
		   lxml \
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

COPY requirements.txt /stack-requirements.txt
RUN pip install --no-cache-dir -r stack-requirements.txt
# Set the timezone.
RUN  echo "Asia/Shanghai" > /etc/timezone
RUN  dpkg-reconfigure -f noninteractive tzdata
# Add crontab file in the cron directory
ADD crontab /etc/cron.d/hello-cron
 
# Give execution rights on the cron job
RUN chmod 0644 /etc/cron.d/hello-cron
 
# Create the log file to be able to run tail
RUN touch /var/tempcron.log
ENV PATH "/code:${PATH}" 
# Run the command on container startup
CMD cron && tail -f /var/tempcron.log
#CMD cron
