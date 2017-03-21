# Download base image Debian testing (Slim).
FROM debian:testing-slim

# Set Environements Variables.
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV JAVA_AWT_INCLUDE_PATH /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/
ENV JAVA_INCLUDE_PATH /usr/lib/jvm/java-8-openjdk-amd64/include
ENV JAVA_INCLUDE_PATH2 /usr/lib/jvm/java-8-openjdk-amd64/include/linux
ENV JAVA_AWT_LIBRARY /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/libjawt.so
ENV JAVA_JVM_LIBRARY /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/server/libjvm.so
ENV OSPL_URL file:///usr/etc/opensplice/config/ospl.xml
ENV DEBIAN_FRONTEND noninteractive

# Install base stack packages.
RUN apt-get update && apt-get install -q -y --no-install-recommends --no-install-suggests gnupg git wget apt-utils locales
RUN touch /usr/share/locale/locale.alias && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

# ROS Repo Stack ##############################################################

# Setup Key.
#RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 421C365BD9FF1F717815A3895523BAEEB01FA116
RUN /usr/bin/wget -qO - http://packages.ros.org/ros.key | apt-key add -

# Setup sources list.
RUN echo "deb http://packages.ros.org/ros/ubuntu jessie main" > /etc/apt/sources.list.d/ros-latest.list

# OSRF Repo Stack ##############################################################

# Setup keys
#RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys D2486D2DD83DB69272AFE98867170598AF249743
RUN /usr/bin/wget -qO - http://packages.osrfoundation.org/gazebo.key | apt-key add -

# Setup sources list.
#RUN echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable jessie main" > /etc/apt/sources.list.d/gazebo-latest.list

# Create default path for man.
RUN mkdir -p /usr/share/man/man1

# Install ROS-java dependancy.
RUN apt-get update && apt-get install -q -y --no-install-recommends --no-install-suggests \
    gradle openjdk-8-jdk openjdk-8-jdk-headless openjdk-8-jre openjdk-8-jre-headless libhawtjni-runtime-java \
    build-essential cppcheck cmake libopencv-dev libpoco-dev libpocofoundation9v5 libpocofoundation9v5-dbg python-empy python3-dev python3-empy python3-nose python3-pip python3-setuptools python3-vcstool \
    clang-format pydocstyle pyflakes python3-coverage python3-mock python3-pep8 uncrustify \
    libboost-chrono-dev libboost-date-time-dev libboost-program-options-dev libboost-regex-dev libboost-system-dev libboost-thread-dev \
    pyflakes
#    libopensplice64

# Tempory Gradle.
RUN /usr/bin/wget https://launchpad.net/~cwchien/+archive/ubuntu/gradle/+files/gradle-2.14.1_1.0-0ubuntu1_all.deb && dpkg -i gradle-2.14.1_1.0-0ubuntu1_all.deb

# Clean tempories files.
RUN rm -rf /var/lib/apt/lists/*

# Create default Workspace.
RUN mkdir -p /home/travis/build/ament_ws/src
RUN mkdir -p /home/travis/build/ros2_java_ws/src
RUN cd /home/travis/build

# Run commans
CMD echo "It's work... !"
