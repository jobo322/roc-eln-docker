FROM node:7-slim

# Install Apache
RUN apt-get update && apt-get install -y apache2 cron git
EXPOSE 80

# Get flavor-builder
WORKDIR /git/flavor-builder
COPY package.json package.json
RUN yarn && rm -rf /root/.npm /usr/local/share/.cache /root/.cache

COPY crontab /etc/cron.d/flavor-cron
RUN chmod 744 /etc/cron.d/flavor-cron

COPY start.sh /start.sh
RUN chmod 744 /start.sh

COPY www /var/www/html

COPY on-tabs-config.json /on-tabs-config.json
RUN node /git/flavor-builder/node_modules/visualizer-on-tabs/bin/build.js --outDir=/var/www/html/on-tabs/ --config=/on-tabs-config.json

COPY flavor-config.json /flavor-config.json

CMD /start.sh
