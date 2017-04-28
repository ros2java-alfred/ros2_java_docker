# Download base image Debian testing (Slim).
FROM debian:testing-slim

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION="1.0.3"

LABEL maintainer="Mickael Gaillard <mick.gaillard@gmail.com>" \
      version="$VERSION" \
      description="ROS2 for java" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="ROS2java" \
      org.label-schema.description="" \
      org.label-schema.url="https://github.com/ros2java-alfred/ros2_java_docker" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/ros2java-alfred/ros2_java_docker" \
      org.label-schema.vendor="ROS2java-Alfred" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

# Set Environements Variables.
ENV INITRD                  no \
    DEBIAN_FRONTEND         noninteractive \
    JAVA_HOME               /usr/lib/jvm/java-8-openjdk-amd64 \
    JAVA_AWT_INCLUDE_PATH   /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/ \
    JAVA_INCLUDE_PATH       /usr/lib/jvm/java-8-openjdk-amd64/include \
    JAVA_INCLUDE_PATH2      /usr/lib/jvm/java-8-openjdk-amd64/include/linux \
    JAVA_AWT_LIBRARY        /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/libjawt.so \
    JAVA_JVM_LIBRARY        /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/server/libjvm.so \
    OSPL_URL                file:///usr/etc/opensplice/config/ospl.xml

ARG APT_FLAGS="-q -y --no-install-recommends --no-install-suggests"

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

ENV LANG en_US.UTF-8

# ROS2 Build Stack ##############################################################

# apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 421C365BD9FF1F717815A3895523BAEEB01FA116
# apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys D2486D2DD83DB69272AFE98867170598AF249743
# echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable jessie main" > /etc/apt/sources.list.d/gazebo-latest.list

RUN /usr/bin/wget -qO - http://packages.ros.org/ros.key | apt-key add - && \
    /usr/bin/wget -qO - http://packages.osrfoundation.org/gazebo.key | apt-key add - && \
    echo "deb http://packages.ros.org/ros/ubuntu jessie main" > /etc/apt/sources.list.d/ros-latest.list && \
    apt-get update && \
    apt-get install ${APT_FLAGS} \
        gradle \
        openjdk-8-jdk \
        openjdk-8-jdk-headless \
        openjdk-8-jre \
        openjdk-8-jre-headless \
        libhawtjni-runtime-java \
        git \
        wget \
        build-essential \
        cppcheck \
        cmake \
        libopencv-dev \
        libpoco-dev \
        python-empy \
        python3-empy \
        python3-setuptools \
        python3-nose \
        python3-pip \
        python3-vcstool \
        libtinyxml-dev \
        libeigen3-dev \
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
        pydocstyle \
        clang-format \
        python3-dev \
        libpocofoundation46 && \
    rm -rf /var/lib/apt/lists/*

#    libopensplice64

# Create default Workspace.
RUN mkdir -p /home/travis/build/ament_ws/src && \
    mkdir -p /home/travis/build/ros2_java_ws/src

# Run commans
CMD echo "Welcome to Debian Testing GNU/linux for ROS2 Java"
