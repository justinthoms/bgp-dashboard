FROM ubuntu:22.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y \
        python3 \
        python3-pip \
        python3-dev \
        uwsgi-plugin-python3 \
        nginx \
        supervisor && \
    echo 'Etc/UTC' >/etc/timezone && \
    apt-get install -y --reinstall tzdata && \
    rm -rf /var/lib/apt/lists/*

COPY nginx/flask.conf /etc/nginx/sites-available/
COPY supervisor/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY app/requirements.txt /tmp/requirements.txt

RUN mkdir -p /var/log/nginx/app /var/log/uwsgi/app /var/log/supervisor /var/www/app && \
    rm /etc/nginx/sites-enabled/default && \
    ln -s /etc/nginx/sites-available/flask.conf /etc/nginx/sites-enabled/flask.conf && \
    echo "daemon off;" >> /etc/nginx/nginx.conf && \
    pip3 install -r /tmp/requirements.txt && \
    chown -R www-data:www-data /var/www/app && \
    chown -R www-data:www-data /var/log

CMD ["/usr/bin/supervisord"]
