FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app
COPY . .
RUN dotnet publish src/Gateway/FeedR.Gateway -c release -o out
# this can work but will have errors when using Shared
# RUN dotnet publish FeedR.Gateway -c release -o out

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .
ENV ASPNETCORE_URLS http://*:80
ENV ASPNETCORE_ENVIRONMENT docker
ENTRYPOINT dotnet FeedR.Gateway.dll

# build image
# if we have this: RUN dotnet publish FeedR.Gateway -c release -o out
# then:
# docker build -t feedr-gateway .
# however now we have this: RUN dotnet publish src/Gateway/FeedR.Gateway -c release -o out
# so:
# docker build -t feedr-gateway -f src/Gateway/Dockerfile .

# run container
# docker run --rm -it -p 5000:80 feedr-gateway