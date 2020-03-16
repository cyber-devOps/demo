#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["asp/asp.csproj", "asp/"]
RUN dotnet restore "asp/asp.csproj"
COPY . .
WORKDIR "/src/asp"
RUN dotnet build "asp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "asp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "asp.dll"]