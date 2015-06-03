FROM concourse/concourse-ci:latest

RUN apt-get update -y && apt-get -y install dnsutils
ADD bin/* /usr/local/testutils/bin/
ADD etc/* /usr/local/testutils/etc/
ADD ssh/* /usr/local/testutils/ssh/
