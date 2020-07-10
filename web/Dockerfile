FROM node:12

MAINTAINER ${PROJECT_MAINTAINER}

CMD [ "node"]

# Install custom entrypoint
COPY ./entrypoint.sh /usr/local/bin/docker-custom-entrypoint
RUN chmod 777 /usr/local/bin/docker-custom-entrypoint

RUN npm install -g nodemon

RUN cd ${PROJECT_PATH} && npm install

ADD bash_aliases /root/.bashrc
ENV TERM xterm

ENTRYPOINT ["docker-custom-entrypoint"]
