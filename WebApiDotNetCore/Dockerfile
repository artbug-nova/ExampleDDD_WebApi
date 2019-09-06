FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["WebApiDotNetCore/WebApiDotNetCore.csproj", "WebApiDotNetCore/"]
RUN dotnet restore "WebApiDotNetCore/WebApiDotNetCore.csproj"
COPY . .
WORKDIR "/src/WebApiDotNetCore"
RUN dotnet build "WebApiDotNetCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApiDotNetCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApiDotNetCore.dll"]