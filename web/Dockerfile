############################################################
# Dockerfile to build a node.js v. 6 development
# Based on Ubuntu
############################################################

# Set the base image
FROM node:6

# File Author / Maintainer
MAINTAINER thajo

# Should run commands as non root if going to production!!!

# Since we want to use the cache when building new containers
# Trick taken from: http://bitjudo.com/blog/2014/03/13/building-efficient-dockerfiles-node-dot-js/
ADD app/package.json /tmp/package.json

# Just the modules needed in production
RUN cd /tmp && npm install --production

# create an app folder
RUN mkdir -p /opt/app && cp -a /tmp/node_modules /opt/app/

# no need in production
#VOLUME /opt/app/node_modules


# Set enviroment to production
ENV NODE_ENV=production

# install process manager (PM2)
RUN npm install pm2 -g

# copy the the
COPY app/ /opt/app/.

# Clean up
RUN rm -rf /opt/app/test
RUN rm -rf /opt/app/script
RUN rm  /opt/app/.jscsrc
RUN rm  /opt/app/.jshintrc

# if needed?
#COPY docker-entrypoint.sh /
#ENTRYPOINT ["/docker-entrypoint.sh"]

## Logs?
EXPOSE 7000

# Run app
CMD ["pm2-docker", "/opt/app/src/index.js"]
