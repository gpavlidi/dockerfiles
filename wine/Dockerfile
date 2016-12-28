FROM debian:jessie
MAINTAINER Yanis Pavlidis <yanis@pavlidis.email>

RUN echo 'deb http://httpredir.debian.org/debian jessie-backports main' > /etc/apt/sources.list.d/jessie-backports.list \
	# enable multiarch
	&& dpkg --add-architecture i386 && apt update \
	# install wine 32 and 64 bits and usual suspects
	&& apt install -y --no-install-recommends \
		wine/jessie-backports \
		wine32/jessie-backports \
		wine64/jessie-backports \
		libwine/jessie-backports \
		libwine:i386/jessie-backports \
		fonts-wine/jessie-backports \
		cabextract \
		unzip \
		zenity \
		libgl1-mesa-dri \
		libgl1-mesa-glx \
		libasound2 \
		alsa-utils \
		xvfb \
		xauth \
		curl \
		nano \
		less \
		ca-certificates \
		mesa-utils \
		pciutils \
		mingw-w64 git cmake \
# install gecko
	&& mkdir -p /usr/share/wine/gecko \
		&& curl -SL http://dl.winehq.org/wine/wine-gecko/2.40/wine_gecko-2.40-x86.msi -o /usr/share/wine/gecko/wine_gecko-2.40-x86.msi \
		&& curl -SL http://dl.winehq.org/wine/wine-gecko/2.40/wine_gecko-2.40-x86_64.msi -o /usr/share/wine/gecko/wine_gecko-2.40-x86_64.msi \
		&& chmod +x /usr/share/wine/gecko/*.msi \
# install mono
	&& mkdir -p /usr/share/wine/mono \
		&& curl -SL 'http://sourceforge.net/projects/wine/files/Wine%20Mono/4.5.6/wine-mono-4.5.6.msi/download' -o /usr/share/wine/mono/wine-mono-4.5.6.msi\
		&& chmod +x /usr/share/wine/mono/wine-mono-4.5.6.msi \
# install winetricks
	&& curl -SL 'https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks' -o /usr/local/bin/winetricks \
		&& chmod +x /usr/local/bin/winetricks \
# cleanup
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Wine really doesn't like to be run as root, so let's use a non-root user
#RUN useradd -ms /bin/bash wineuser
#USER wineuser
#ENV HOME /home/wineuser
#ENV WINEPREFIX /home/wineuser/.wine
#ENV WINEARCH win32
#WORKDIR /home/wineuser

# Generate wine settings for both 32/64 bits installation, waiting for wineserver to finish
ENV WINEPREFIX /root/.wine
RUN xvfb-run wine "wineboot" && while pgrep -u `whoami` wineserver > /dev/null; do sleep 1; done
RUN WINEARCH=win32 WINEPREFIX=/root/.wine32 xvfb-run wine "wineboot" && while pgrep -u `whoami` wineserver > /dev/null; do sleep 1; done
RUN echo 'alias WIN32="WINEARCH=win32 WINEPREFIX=/root/.wine32"' >> ~/.bashrc
RUN echo 'alias WIN64="WINEARCH=win64 WINEPREFIX=/root/.wine"' >> ~/.bashrc

# prepare directory structure
WORKDIR /root
ENV HOME /root
ENV LANG en-US

ENTRYPOINT [ "wine" ]