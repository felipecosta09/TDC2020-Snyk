#FROM maven:3-alpine

FROM maven:3-jdk-8-alpine

COPY fake-rhel.tgz /

RUN tar -zxvf fake-rhel.tgz

# This will trigger at least 3 medium vulnerabilities in apache2
COPY lib-apk-db-installed /lib/apk/db/installed

# This will trigger the checklist scanner
# COPY /fake-rhel / 

# This will trigger an oscap finding for wordpress
COPY wpversion /fake/wp-includes/version.php

# This will trigger a malware finding
ADD https://secure.eicar.org/eicar.com /eicar.com

# This will trigger a content finding for a private key in PEM format
COPY cert.pem /cert.pem

RUN mkdir /tmp/extracted_files

COPY . /usr/src/goof
WORKDIR /usr/src/goof

RUN mvn install

EXPOSE 8080

ENTRYPOINT ["mvn", "tomcat7:run"]