FROM httpd:2.4.46@sha256:ef3702048ce3297435fa12a44f5a29d9541a94f1fb84537b5192872fa64d8c1f
# "Created": "2021-04-10T12:29:59.638214089Z" , "Version":"2.4.46"

RUN apt-get update \
  && apt-get install -y --no-install-recommends wget ca-certificates libcjose0 libhiredis0.14 apache2-api-20120211 apache2-bin\
  && wget https://github.com/zmartzone/mod_auth_openidc/releases/download/v2.4.8.2/libapache2-mod-auth-openidc_2.4.8.2-1.buster+1_amd64.deb \
  && dpkg -i libapache2-mod-auth-openidc_2.4.8.2-1.buster+1_amd64.deb \
  && ln -s /usr/lib/apache2/modules/mod_auth_openidc.so /usr/local/apache2/modules/mod_auth_openidc.so \
  && rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt \
  && touch /usr/local/apache2/conf/extra/secret.conf \
  && touch /usr/local/apache2/conf/extra/oidc.conf

RUN echo "\n\nLoadModule auth_openidc_module modules/mod_auth_openidc.so\n\nInclude conf/extra/secret.conf\nInclude conf/extra/oidc.conf\n" >> /usr/local/apache2/conf/httpd.conf
