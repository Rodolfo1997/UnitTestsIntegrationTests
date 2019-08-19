FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["UnitAndIntegrationTests.API/UnitAndIntegrationTests.API.csproj", "UnitAndIntegrationTests.API/"]
RUN dotnet restore "UnitAndIntegrationTests.API/UnitAndIntegrationTests.API.csproj"
COPY . .
WORKDIR "/src/UnitAndIntegrationTests.API"
RUN dotnet build "UnitAndIntegrationTests.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "UnitAndIntegrationTests.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "UnitAndIntegrationTests.API.dll"]