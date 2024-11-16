FROM ubuntu:20.04

RUN apt-get update -y && \
	apt-get upgrade -y && \
	apt-get install -y curl git unzip xz-utils zip libglu1-mesa

# Install Chrome
RUN apt-get install -y wget gnupg && \
	rm -rf /var/lib/apt/lists/* && \
	wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
	echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends google-chrome-stable && \
	rm -rf /var/lib/apt/lists/*

RUN apt-get clean

# Install Flutter SDK
ENV FLUTTER_CHANNEL="stable"
ENV FLUTTER_VERSION="3.24.5"
ENV FLUTTER_HOME=/opt/flutter
ENV PATH=${PATH}:${FLUTTER_HOME}/bin

RUN cd /opt \
	&& curl -C - --output flutter.tar.xz https://storage.googleapis.com/flutter_infra_release/releases/${FLUTTER_CHANNEL}/linux/flutter_linux_${FLUTTER_VERSION}-${FLUTTER_CHANNEL}.tar.xz \
	&& tar xf flutter.tar.xz -C . \
	&& rm flutter.tar.xz

RUN git config --global --add safe.directory /opt/flutter

RUN flutter config --no-analytics \
	&& flutter config --enable-web \
	&& flutter update-packages
