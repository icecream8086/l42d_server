# https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/9/html/building_running_and_managing_containers/proc_building-ubi-based-images_assembly_adding-software-to-a-ubi-container
# https://www.bilibili.com/read/cv16824745/#:~:text=%E6%B1%82%E7%94%9F%E4%B9%8B%E8%B7%AF2%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%90%AD%E5%BB%BA%EF%BC%88Linux-CentOS%EF%BC%89%201%201%20%E5%89%8D%E8%A8%80%26%E7%9B%AE%E5%BD%95%201.1%20%E5%89%8D%E8%A8%80%202%202,%E6%AD%A4%E9%83%A8%E5%88%86%E5%86%85%E5%AE%B9%E8%BD%AC%E7%A7%BB%E5%88%B0%E5%8F%A6%E4%B8%80%E7%AF%87%E4%B8%93%E6%A0%8F%EF%BC%9A%20screen%20%E4%BB%8B%E7%BB%8D%E5%92%8C%E7%94%A8%E6%B3%95%207%207%20%E8%A1%A5%E5%85%85%E8%AF%B4%E6%98%8E%207.1%20%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%B8%B8%E8%A7%81%E6%95%85%E9%9A%9C%E7%9A%84%E5%A4%84%E7%90%86%E5%8A%9E%E6%B3%95
FROM registry.access.redhat.com/ubi9/ubi
USER root
LABEL maintainer="John Doe"
# Update image
RUN yum update --disablerepo=* --enablerepo=ubi-9-appstream-rpms --enablerepo=ubi-9-baseos-rpms -y && rm -rf /var/cache/yum
RUN yum install --disablerepo=* --enablerepo=ubi-9-appstream-rpms --enablerepo=ubi-9-baseos-rpms httpd wget -y && rm -rf /var/cache/yum
# Install glibc.i686 and libstdc++.i686
RUN yum install glibc.i686 libstdc++.i686 -y && rm -rf /var/cache/yum
# Add user steam and set password
RUN useradd steam && echo steam:99999 | chpasswd
USER steam
WORKDIR /home/steam
# Download, extract, install SteamCMD, and remove the installation package
RUN wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz && \
    tar xvf steamcmd_linux.tar.gz && \
    rm steamcmd_linux.tar.gz
# Create a script to install and validate l4d2
RUN echo -e 'force_install_dir ./l4d2server\nlogin anonymous\napp_update 222860 validate\nexit' > steamcmd_script.txt && \
    ./steamcmd.sh +runscript steamcmd_script.txt
# Create server.cfg
RUN echo -e 'rcon_password ""\nsv_password ""\nsv_allow_lobby_connect_only 0\nsv_tags hidden\nsv_gametypes "coop,versus,survival"\nmp_gamemode coop\nz_difficulty Normal\nsv_region 4\nsv_lan 0\nsv_consistency 0\nsv_cheats 0\nmotd_enabled 1' > ./l4d2server/left4dead2/cfg/server.cfg
# Create start.sh and give it execute permissions
RUN echo -e '#!/bin/bash\n/home/steam/l4d2server/srcds_run -game left4dead2 -insecure +map c1m2_streets -condebug +exec server.cfg -nomaster' > ./l4d2server/start.sh && \
    chmod +x ./l4d2server/start.sh
# Expose the necessary port
EXPOSE 27015
# Start the l4d2 server
CMD ["./l4d2server/start.sh"]