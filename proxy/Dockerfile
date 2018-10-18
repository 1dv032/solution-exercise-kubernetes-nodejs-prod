############################################################
# Dockerfile to build Nginx Installed Containers
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu

# File Author / Maintainer
MAINTAINER thajo

# Install Nginx

# Update the repository
RUN apt-get update

# Install necessary tools
RUN apt-get install -y nano wget dialog net-tools

# Download and Install Nginx
RUN apt-get install -y nginx

# Add the web-data user to own the source
RUN chown -R www-data:www-data /var/lib/nginx

# Add our custom nginx config that configs the nginx server
RUN rm -v /etc/nginx/nginx.conf
ADD nginx-sites.conf /etc/nginx/nginx.conf

# Append "daemon off;" to the beginning of the configuration
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Expose ports
EXPOSE 80
EXPOSE 443

# The self singed certificate is created before through the script
COPY ./sslcerts/cert.pem /etc/ssl/mydomainA_cert.pem
COPY ./sslcerts/key.pem /etc/ssl/mydomainA_key.pem

# Set the default command to execute
# when creating a new container
CMD service nginx start
