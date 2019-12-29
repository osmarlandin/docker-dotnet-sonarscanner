FROM mcr.microsoft.com/dotnet/core/sdk:3.0-disco as build-environment

RUN apt-get install wget
RUN apt-get install gpg

RUN apt-get update

RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg && \
mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ && \
wget -q https://packages.microsoft.com/config/debian/9/prod.list && \
mv prod.list /etc/apt/sources.list.d/microsoft-prod.list && \
chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg && \
chown root:root /etc/apt/sources.list.d/microsoft-prod.list

RUN apt-get install apt-transport-https

RUN apt-get update && \
apt-get install -y aspnetcore-runtime-2.1=2.1.0-1

RUN apt-get update && \
   apt-get install -y openjdk-8-jre && \
   apt-get clean;

# Fix certificate issues
RUN apt-get update && \
   apt-get install ca-certificates-java && \
   apt-get clean && \
   update-ca-certificates -f;

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN dotnet tool install -g dotnet-sonarscanner
ENV PATH="${PATH}:/root/.dotnet/tools"
