FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["BV212_ASP.NET_CORE_Autodrom_1/BV212_ASP.NET_CORE_Autodrom_1.csproj", "BV212_ASP.NET_CORE_Autodrom_1/"]
RUN dotnet restore "BV212_ASP.NET_CORE_Autodrom_1/BV212_ASP.NET_CORE_Autodrom_1.csproj"
COPY . .
WORKDIR "/src/BV212_ASP.NET_CORE_Autodrom_1"
RUN dotnet build "BV212_ASP.NET_CORE_Autodrom_1.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "BV212_ASP.NET_CORE_Autodrom_1.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BV212_ASP.NET_CORE_Autodrom_1.dll"]
