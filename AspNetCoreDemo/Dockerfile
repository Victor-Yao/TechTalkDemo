# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# copy csproj and restore as distinct layers
WORKDIR /source
COPY *.csproj .
RUN dotnet restore --use-current-runtime  

# copy everything else and build app
COPY . .
RUN dotnet publish -c Release -o /app

EXPOSE 80
# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "AspNetCoreDemo.dll"]
