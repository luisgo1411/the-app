FROM consol/ubuntu-xfce-vnc:latest

ENV http_proxy=${http_proxy} \
    https_proxy=${https_proxy} \
    no_proxy="${no_proxy}"
    
COPY ./vagrant/provision/roles/vnc/files/dojo.jpg ./dojo.jpg

COPY ./vagrant/provision/roles/vnc/templates/xfce4-desktop.xml ./.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-desktop.xml

COPY ./vagrant/provision/roles/vnc/files/dojo.profile.tgz ./dojo.profile.tgz

#RUN tar -xvzf dojo.profile.tgz