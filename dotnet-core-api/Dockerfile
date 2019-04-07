FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["dotnet-core-api/dotnet-core-api.csproj", "dotnet-core-api/"]
RUN dotnet restore "dotnet-core-api/dotnet-core-api.csproj"
COPY . .
WORKDIR "/src/dotnet-core-api"
RUN dotnet build "dotnet-core-api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "dotnet-core-api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dotnet-core-api.dll"]