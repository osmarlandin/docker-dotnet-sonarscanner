# docker-dotnet-sonarscanner
This repository contains `Dockerfile` definitions for an image used for building dotnet core projects using sonarscanner

## Supported tags

- [`2.1-sdk`](https://hub.docker.com/r/osmarlandin/dotnet-sonarscanner/tags/)


## How to use it

Use this image as a base image for building your dotnet core projects

````powershell
FROM osmarlandin/dotnet-sonarscanner:2.1-sdk as build-environment
WORKDIR /app
COPY . .

RUN dotnet restore YourProject.sln
RUN dotnet sonarscanner begin /k:"your-project-key" /d:sonar.host.url="http://your-sonar-url" /d:sonar.cs.opencover.reportsPaths="/app/tests.unit/coverage.opencover.xml"
RUN dotnet build
RUN dotnet test --no-build /p:CollectCoverage=true /p:CoverletOutputFormat=true /p:CoverletOutputFormat="opencover" ./tests.unit/Tests.Unit.csproj
RUN dotnet sonarscanner end
````