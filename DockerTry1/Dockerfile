#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["DockerTry1.csproj", ""]
RUN dotnet restore "./DockerTry1.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DockerTry1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerTry1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerTry1.dll"]
