The Dockerfile code contains the following,

The base OS image is defined in FROM

The maintainer of the docker in MAINTAINER

The Android SDK tools is update after evey new release. With every new update the version number in the download link is updated. Having a variable ENV VERSION_SDK_TOOLS for the version number reduces the effort in long run for maintaining the Dockerfile.

ENV ANDROID_HOME is used for storing sdk folder name.

ENV PATH is used for storing the android sdk tools path.

DEBIAN_FRONTEND is used for installing the packages in Docker.

RUN apt-get -qq update and the consecutive commands are used to update the packages and install packages.

RUN rm -f /etc/ssl/certs/java/cacerts; is used for java ceritifcate.

RUN curl -s https://dl.google.com/android/repository/sdk-tools-linux-${VERSION_SDK_TOOLS}.zip for downloading the Android SDK tools

RUN mkdir -p $ANDROID_HOME/licenses/ is used for creating a directory to accept Android SDK license during installation of Android SDK Tools.

ADD packages.txt /sdk this command adds the file packages.txt ti the sdk folder.

The packages.txt contains the additional packages such as Google play services to be installed.

Create a new file in the repository and name it as

  packages.txt
  
and add the following code,
<pre><code>
    add-ons;addon-google_apis-google-24
    build-tools;26.0.2
    extras;android;m2repository
    extras;google;m2repository
    extras;google;google_play_services
    extras;m2repository;com;android;support;constraint; constraint-layout;1.0.2
    extras;m2repository;com;android;support;constraint; constraint-layout-solver;1.0.2
    platform-tools
    platforms;android-26
</code></pre>
RUN mkdir -p /root/.android && is used to create a folder and the subsequent commands are used to update the Android SDK.

RUN while read -r package; do PACKAGES="${PACKAGES}${package} is used to run the packages.txt file. Next, the packages are downloaded and installed.

