## 🐟 Docker-Dotnet-Sample 🚀
This is a simple project to demonstrate how to use docker with .NET Core 7.0


🎃 **Dockerfile - Multi-stage builds**
```
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app
EXPOSE 5237
EXPOSE 7106

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /source
COPY /*.csproj .
RUN dotnet restore dotnet-docker.csproj
COPY . .
RUN dotnet build -c Release -o /app/build

FROM build AS publish
RUN dotnet publish -c Release -o /app/published

FROM runtime AS final 
COPY --from=publish /app/published .
CMD ["dotnet", "dotnet-docker.dll"]
```
 🫀 **To create and run a new container just run the command below**
```
docker run -d -p 5237:5237 -p 7106:7106 -e ASPNETCORE_HTTP_PORT=https://+:7106 -e ASPNETCORE_URLS=http://+:5237  --name dotnet-docker dotnet-docker
```
