FROM centos:7.4.1708
ENV NGINX_VERSION="1.20.0 (nginx-plus-r20)"

COPY app-protect.repo /etc/yum.repos.d/
RUN yum install -y epel-release --nogpgcheck
RUN yum install -y app-protect-88a9be14
RUN yum install -y sudo

# Forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log && \
# Change pid file location & remove nginx user & change port to 8080
    rm -rf /etc/nginx/nginx.conf


# forward nginx access and error logs to stdout and stderr of the ingress
# controller process
RUN ln -sf /proc/1/fd/1 /var/log/nginx/access.log \
  && ln -sf /proc/1/fd/1 /var/log/nginx/stream-access.log \
  && ln -sf /proc/1/fd/2 /var/log/nginx/error.log

RUN  mkdir -p /var/lib/nginx \
  && mkdir -p /etc/nginx/secrets \
  && mkdir -p /etc/nginx/waf \
  && mkdir -p /var/log/f5waf \
  && mkdir -p /opt/f5waf \
  && chown -R 999:998 /etc/nginx/secrets \
  && chown -R 999:998 /etc/nginx/waf \
  && chown -R 999:998 /etc/nginx \
  && chown -R 999:998 /var/cache/nginx \
  && chown -R 999:998 /var/lib/nginx/ \
  && chown -R 999:998 /var/log/f5waf/ \
  && chown -R 999:998 /opt/f5waf/ \
  && rm /etc/nginx/conf.d/*

COPY log-default.json /etc/nginx
RUN chown 999:998 /etc/nginx/log-default.json

EXPOSE 8080 8443

COPY nginx-ingress /
COPY internal/configs/version1/nginx-plus.ingress.tmpl /
COPY internal/configs/version1/nginx-plus.tmpl /
COPY internal/configs/version2/nginx-plus.virtualserver.tmpl  /
#COPY waf-policy.json /etc/nginx/waf
#RUN chown 999:998 /etc/nginx/waf/waf-policy.json

# Uncomment the line below if you would like to add the default.pem to the image
# and use it as a certificate and key for the default server
ADD default.pem /etc/nginx/secrets/default

ADD protect_start.sh /
RUN echo 'nginx ALL=(ALL) NOPASSWD:ALL' | sudo EDITOR='tee -a' visudo
RUN chmod +x /protect_start.sh

ENTRYPOINT ["/protect_start.sh"]
