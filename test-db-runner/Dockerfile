FROM mcr.microsoft.com/mssql/server:2019-latest
MAINTAINER Jason HyunWoo Kang, https://github.com/KangDroid

ARG DB_PASSWORD helloWorld@

ENV SA_PASSWORD $DB_PASSWORD
ENV ACCEPT_EULA Y
EXPOSE 1433

USER root
RUN sed -i 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y gnupg curl apt-transport-https
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/20.04/mssql-server-2019.list | tee /etc/apt/sources.list.d/mssql-server.list
RUN apt-get update
RUN apt-get install -y mssql-server-ha mssql-server-fts

RUN (/opt/mssql/bin/sqlservr --accept-eula & ) | grep -q "Service Broker manager has started" && /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P testPassword@ -Q "CREATE DATABASE [kdr-test]"
