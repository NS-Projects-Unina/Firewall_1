#Dockerfile per server ftp (aggiungo il pacchetto di eseguibili net-tools)

FROM emalderson/ftplab:ftp_1.0

LABEL maintainer "alf_99@hotmail.it"

RUN apt-get update && apt-get install -y \
net-tools

CMD echo "Dockerfile FTP server"
