FROM node:6.11-alpine

WORKDIR "/opt"

RUN apk add --update git make g++ && \
    git clone https://bitbucket.org/designisdead/blockchain-explorer.git

WORKDIR "/opt/blockchain-explorer"
RUN git checkout c6e12f1 && \
    npm install

ARG mainchain_rpc
RUN sed -i "s/localhost:8545/${mainchain_rpc}/g" views/layout/default_layout.jade && \
    sed -i "s/web3.js/web3.js@0.20.6/g" views/layout/default_layout.jade && \
    grep -lr -e ' ETH' * | xargs sed -i 's/ ETH/ UND/g' && \
    grep -lr -e 'Ethereum' * | xargs sed -i 's/Ethereum/UND/g'  && \
    grep -lr -e 'Ether' * | xargs sed -i 's/Ether/UND/g' && \
    grep -lr -e 'Expolorer' * | xargs sed -i 's/Expolorer/DEMONET Explorer/g' && \
    grep -rl -e '(ethusd' * | xargs sed -i 's/(ethusd/(0.1/g'

CMD npm run start
