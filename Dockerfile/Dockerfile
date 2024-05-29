FROM registry.access.redhat.com/ubi9/ubi
USER root
LABEL maintainer="John Doe"
# Update image
RUN yum update --disablerepo=* --enablerepo=ubi-9-appstream-rpms --enablerepo=ubi-9-baseos-rpms -y && rm -rf /var/cache/yum
RUN yum install --disablerepo=* --enablerepo=ubi-9-appstream-rpms --enablerepo=ubi-9-baseos-rpms httpd -y && rm -rf /var/cache/yum
# Add default Web page and expose port
RUN echo "The Web Server is Running" > /var/www/html/index.html
EXPOSE 80
# Start the service
CMD ["-D", "FOREGROUND"]
ENTRYPOINT ["/usr/sbin/httpd"]

# https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/9/html/building_running_and_managing_containers/proc_building-ubi-based-images_assembly_adding-software-to-a-ubi-container
