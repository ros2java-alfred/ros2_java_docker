# Download base image Ubuntu rolling.
FROM ubuntu:rolling

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION="1.0.3"
ARG APT_FLAGS="-q -y --no-install-recommends --no-install-suggests"

LABEL maintainer="Mickael Gaillard <mick.gaillard@gmail.com>" \
      version="$VERSION-ubuntu-rolling" \
      description="ROS2 for java" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="ROS2java" \
      org.label-schema.description="ROS2 for java" \
      org.label-schema.url="https://github.com/ros2java-alfred/ros2_java_docker" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/ros2java-alfred/ros2_java_docker" \
      org.label-schema.vendor="ROS2java-Alfred" \
      org.label-schema.version="$VERSION-ubuntu-rolling" \
      org.label-schema.schema-version="1.0"

# Set Environements Variables.
ENV INITRD="no" \
    DEBIAN_FRONTEND="noninteractive" \
    JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64" \
    JAVA_AWT_INCLUDE_PATH="/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/" \
    JAVA_INCLUDE_PATH="/usr/lib/jvm/java-8-openjdk-amd64/include" \
    JAVA_INCLUDE_PATH2="/usr/lib/jvm/java-8-openjdk-amd64/include/linux" \
    JAVA_AWT_LIBRARY="/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/libjawt.so" \
    JAVA_JVM_LIBRARY="/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/server/libjvm.so" \
    OSPL_URL="file:///usr/etc/opensplice/config/ospl.xml"

# Base Build Stack ##############################################################

RUN apt-get update && \
    apt-get install ${APT_FLAGS} \
        gnupg \
        git \
        curl \
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
    echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list && \
    echo "deb http://packages.osrfoundation.org/gazebo/ubuntu bionic main" > /etc/apt/sources.list.d/gazebo-latest.list && \
    apt-get update && \
    apt-get install ${APT_FLAGS} \
        gradle \
        openjdk-8-jdk \
        openjdk-8-jdk-headless \
        openjdk-8-jre \
        openjdk-8-jre-headless \
        libhawtjni-runtime-java \
        build-essential \
        cppcheck \
        cmake \
        libopencv-dev \
        python-empy \
        python3-catkin-pkg-modules \
        python3-dev \
        python3-empy \
        python3-nose \
        python3-pip \
        python3-pyparsing \
        python3-pytest \
        python3-pytest-cov \
        python3-setuptools \
        python3-vcstool \
        libtinyxml-dev \
        libeigen3-dev \
        libassimp-dev \
        libpoco-dev \
        python3-colcon-common-extensions \
        clang-format \
        pydocstyle \
        pyflakes \
        python3-coverage \
        python3-mock \
        python3-pep8 \
        uncrustify \
        libasio-dev \
        libtinyxml2-dev \
        python3-argcomplete \
        clang \
        libssl-dev \
        openssl && \
    rm -rf /var/lib/apt/lists/*

#    libopensplice64

# Create default Workspace.
RUN mkdir -p /home/travis/build/ament_ws/src && \
    mkdir -p /home/travis/build/ros2_java_ws/src && \
    mkdir -p /home/travis/.gradle && \
    touch /home/travis/.gradle/gradle.properties && \
    echo "org.gradle.jvmargs=-Xmx3072M -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8" | tee -a /home/travis/.gradle/gradle.properties

# Run commans
CMD echo "Welcome to Ubuntu rolling GNU/linux for ROS2 Java"
