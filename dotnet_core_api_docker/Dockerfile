FROM mcr.microsoft.com/dotnet/aspnet:7.0 as base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 as build
WORKDIR /src
COPY ["dotnet_core_api_docker/dotnet_core_api_docker.csproj","dotnet_core_api_docker/"]

RUN dotnet restore "dotnet_core_api_docker/dotnet_core_api_docker.csproj"

COPY . .

WORKDIR "/src/dotnet_core_api_docker"

RUN dotnet build "dotnet_core_api_docker.csproj" -c Release -o /app/build

FROM build as publish

RUN dotnet publish "dotnet_core_api_docker.csproj" -c Release -o /app/publish

FROM base as final

WORKDIR /app

COPY --from=publish /app/publish .

ENTRYPOINT [ "dotnet","dotnet_core_api_docker.dll" ]

