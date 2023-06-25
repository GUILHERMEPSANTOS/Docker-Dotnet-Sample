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