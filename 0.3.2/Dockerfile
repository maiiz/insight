FROM node:0.12

ENV TESTNET 0
ENV VERSION 0.3.2

WORKDIR /opt/insight

RUN apt-get update \
    && apt-get install -y wget \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && apt-get autoclean -y \
    && rm -rf /var/lib/apt/lists/*

#install bitcore-node
RUN npm install -g bitcore-node@2.1.0

ADD . /opt/insight

#create livenet insight
RUN bitcore-node create livenet \
    && cd livenet \
    && bitcore-node install insight-api@0.3.2 \
    && bitcore-node install insight-ui@0.3.1 \
    && mv node_modules ..

#create testnet insight
RUN bitcore-node create -t testnet \
    && cd testnet \
    && bitcore-node install insight-api@0.3.2 \
    && bitcore-node install insight-ui@0.3.1 \
    && rm -rf node_modules

VOLUME /var/lib/insight

RUN chmod 755 run.sh

EXPOSE 3001
CMD ["./run.sh"]
