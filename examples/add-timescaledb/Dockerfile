FROM quay.io/sclorg/postgresql-15-c9s

ADD https://copr.fedorainfracloud.org/coprs/hhorak/timescale4pgsql15/repo/centos-stream-9/hhorak-timescale4pgsql15-centos-stream-9.repo /etc/yum.repos.d/hhorak-timescale4pgsql15-centos-stream-9.repo

USER 0
RUN yum install -y timescaledb && yum clean all
USER 26

RUN mkdir -p /var/lib/pgsql/data/userdata && echo "shared_preload_libraries = 'timescaledb'" >> /var/lib/pgsql/data/userdata/postgresql.conf
ADD . $APP_ROOT/src/
