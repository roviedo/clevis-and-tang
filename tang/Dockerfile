FROM ubuntu:18.04
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN apt-get -y update && apt-get -y install tang && apt-get -y install systemd && apt-get -y install jose && apt-get -y install libjose-dev && apt-get -y install curl

# RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && apt install -y nodejs

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.35.3/install.sh | bash

RUN touch ~/.bashrc && chmod +x ~/.bashrc
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
RUN . ~/.nvm/nvm.sh && source ~/.bashrc && nvm install node

ENV NODE_ENV=production
WORKDIR /app

COPY ["package.json", "package-lock.json*", "./"]

# RUN npm install --production

# RUN nvm install node
# RUN npm install --production

COPY . .

CMD [ "node", "server.js" ]