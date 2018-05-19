
FROM fluent/fluentd:v0.12-debian-onbuild
MAINTAINER josse.santos@ctinmx.net

# default syslog listener port
EXPOSE 10514
# monitor agent port
EXPOSE 24220
# default forwarder port
EXPOSE 24224
# default debug port
EXPOSE 24230

RUN  mkdir -p /var/log/td-agent/ \
     && mkdir -p /var/log/holehole/

RUN buildDeps="sudo make gcc g++ libc-dev ruby-dev" \
 && apt-get update \
 && apt-get install -y --no-install-recommends $buildDeps \
 && sudo gem install \
        fluent-plugin-elasticsearch \
        activesupport \
        public_suffix \
        elasticsearch-transport \
        elasticsearch-api \
        elasticsearch \
        fluentd \
        fluent-plugin-elasticsearch \
        fluent-plugin-kubernetes_metadata_filter \
        fluent-plugin-rewrite-tag-filter \
        fluent-plugin-parser \
        fluent-plugin-grok-parser \
        fluent-plugin-secure-forward \
        fluent-plugin-systemd \
        fluent-plugin-viaq_data_model \
        fluent-plugin-add \
        fluent-plugin-collectd-nest \
        fluent-plugin-out_apache_log_format \

 && sudo gem sources --clear-all \
 && SUDO_FORCE_REMOVE=yes \
    apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
 && rm -rf /var/lib/apt/lists/* \
           /home/fluent/.gem/ruby/2.3.0/cache/*.gem

