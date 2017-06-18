# Download base image Debian stable (Slim).
FROM debian:stable-slim

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION="1.0.3"
ARG APT_FLAGS="-q -y --no-install-recommends --no-install-suggests"

LABEL maintainer="Mickael Gaillard <mick.gaillard@gmail.com>" \
      version="$VERSION-debian-stable" \
      description="ROS2 for java" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="ROS2java" \
      org.label-schema.description="ROS2 for java" \
      org.label-schema.url="https://github.com/ros2java-alfred/ros2_java_docker" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/ros2java-alfred/ros2_java_docker" \
      org.label-schema.vendor="ROS2java-Alfred" \
      org.label-schema.version="$VERSION-debian-stable" \
      org.label-schema.schema-version="1.0"

# Set Environements Variables.
ENV INITRD="no" \
    DEBIAN_FRONTEND="noninteractive" \
    JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64" \
    JAVA_AWT_INCLUDE_PATH="/usr/lib/jvm/java-7-openjdk-amd64/jre/lib/amd64" \
    JAVA_INCLUDE_PATH="/usr/lib/jvm/java-7-openjdk-amd64/include" \
    JAVA_INCLUDE_PATH2="/usr/lib/jvm/java-7-openjdk-amd64/include/linux" \
    JAVA_AWT_LIBRARY="/usr/lib/jvm/java-7-openjdk-amd64/jre/lib/amd64/libjawt.so" \
    JAVA_JVM_LIBRARY="/usr/lib/jvm/java-7-openjdk-amd64/jre/lib/amd64/server/libjvm.so" \
    OSPL_URL="file:///usr/etc/opensplice/config/ospl.xml"

# Base Build Stack ##############################################################

RUN apt-get update && \
    apt-get install ${APT_FLAGS} \
        gnupg \
        git \
        wget \
        apt-utils \
        locales && \
    locale-gen en_US.UTF-8 && \
    touch /usr/share/locale/locale.alias && \
    mkdir -p /usr/share/man/man1 && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    echo 'LANG="en_US.UTF-8"' > /etc/default/locale && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8 && \
    rm -rf /var/lib/apt/lists/*

ENV LANG="en_US.UTF-8"

# ROS2 Build Stack ##############################################################

RUN /usr/bin/wget -qO - http://packages.ros.org/ros.key | apt-key add - && \
    /usr/bin/wget -qO - http://packages.osrfoundation.org/gazebo.key | apt-key add - && \
    echo "deb http://packages.ros.org/ros/ubuntu jessie main" > /etc/apt/sources.list.d/ros-latest.list && \
    echo "deb http://packages.osrfoundation.org/gazebo/debian-stable jessie main" > /etc/apt/sources.list.d/gazebo-latest.list && \
    echo "deb http://httpredir.debian.org/debian jessie-backports main contrib non-free" > /etc/apt/sources.list.d/debian-bp.list && \
    apt-get update && \
    apt-get install ${APT_FLAGS} \
        gradle \
        openjdk-7-jdk \
        openjdk-7-jre \
        openjdk-7-jre-headless \
        libhawtjni-runtime-java \
        build-essential \
        cppcheck \
        cmake \
        libopencv-dev \
        libpoco-dev \
        libpocofoundation9 \
        libpocofoundation9-dbg \
        python-empy \
        python3-dev \
        python3-empy \
        python3-nose \
        python3-pip \
        python3-setuptools \
        python3-vcstool \
        libtinyxml-dev \
        libeigen3-dev \
        clang-format-3.5 \
        pyflakes \
        python3-coverage \
        python3-mock \
        python3-nose \
        python3-pep8 \
        uncrustify \
        libasio-dev \
        libboost-chrono-dev \
        libboost-date-time-dev \
        libboost-program-options-dev \
        libboost-regex-dev \
        libboost-system-dev \
        libboost-thread-dev \
        libboost-thread-dev \
        libtinyxml2-dev \
        libbz2-dev \
        libreadline-dev \
        libsqlite3-dev \
        libusb-1.0-0-dev \
        libudev-dev \
        python3-dev \
        libssl-dev \
        openssl && \
    wget http://ftp.us.debian.org/debian/pool/main/p/pydocstyle/pydocstyle_1.0.0-3_all.deb && \
    dpkg -i ./pydocstyle_1.0.0-3_all.deb && \
    rm -rf ./pydocstyle_1.0.0-3_all.deb && \
    rm -rf /var/lib/apt/lists/*

#    libopensplice64

# Create default Workspace.
RUN mkdir -p /home/travis/build/ament_ws/src && \
    mkdir -p /home/travis/build/ros2_java_ws/src

# Run commans
CMD echo "Welcome to Debian Stable GNU/linux for ROS2 Java"
