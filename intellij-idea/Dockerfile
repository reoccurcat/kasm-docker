FROM kasmweb/core-ubuntu-focal:1.15.0
USER root

ENV HOME /home/kasm-default-profile
ENV STARTUPDIR /dockerstartup
ENV INST_SCRIPTS $STARTUPDIR/install
WORKDIR $HOME

######### Customize Container Here ###########

#RUN apt update >> /dev/null && apt install -y devilspie

#RUN wget "https://github.com/reoccurcat/dotfiles/raw/main/window.ds" -O $HOME/.config/window.ds

RUN wget "https://download.jetbrains.com/idea/ideaIU-2024.2.0.2.tar.gz" -O /tmp/jbidea.tar.gz \
      && tar xf /tmp/jbidea.tar.gz -C /opt

RUN echo "/usr/bin/desktop_ready && /opt/idea-IU*/bin/idea &" > $STARTUPDIR/custom_startup.sh \
      && chmod +x $STARTUPDIR/custom_startup.sh

# Update the desktop environment to be optimized for a single application
RUN cp $HOME/.config/xfce4/xfconf/single-application-xfce-perchannel-xml/* $HOME/.config/xfce4/xfconf/xfce-perchannel-xml/
RUN cp /usr/share/backgrounds/bg_kasm.png /usr/share/backgrounds/bg_default.png
RUN apt-get remove -y xfce4-panel


######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME /home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME

USER 1000
