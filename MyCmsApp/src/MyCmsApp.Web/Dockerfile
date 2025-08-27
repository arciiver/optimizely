# syntax=docker/dockerfile:1

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY nuget.config ./
COPY MyCmsApp.sln ./
COPY *.csproj src/MyCmsApp.Web/
RUN dotnet restore MyCmsApp.sln
COPY . .
RUN dotnet publish MyCmsApp.Web.csproj -c Release -o /app/out /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS run
WORKDIR /app

ENV ASPNETCORE_ENVIRONMENT=Docker
ENV ASPNETCORE_URLS=http://*:80
EXPOSE 80
COPY --from=build /app/out ./

ENTRYPOINT ["dotnet", "MyCmsApp.Web.dll"]
