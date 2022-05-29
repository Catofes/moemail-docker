FROM ubuntu:20.04
RUN apt-get update \
                && apt-get install -y postfix postfix-pgsql postfix-ldap vim less
CMD ["exec","/usr/sbin/postfix","-c","/etc/postfix","start-fg"]