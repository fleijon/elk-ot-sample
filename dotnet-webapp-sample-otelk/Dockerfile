#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["dotnet-webapp-sample-otelk/dotnet-webapp-sample-otelk.csproj", "dotnet-webapp-sample-otelk/"]
RUN dotnet restore "dotnet-webapp-sample-otelk/dotnet-webapp-sample-otelk.csproj"
COPY . .
WORKDIR "/src/dotnet-webapp-sample-otelk"
RUN dotnet build "dotnet-webapp-sample-otelk.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-webapp-sample-otelk.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-webapp-sample-otelk.dll"]