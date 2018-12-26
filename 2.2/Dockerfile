FROM microsoft/dotnet:2.2-sdk as build-environment

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
