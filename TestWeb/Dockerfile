#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /src
COPY ["TestWeb/TestWeb.csproj", "TestWeb/"]
RUN dotnet restore "TestWeb/TestWeb.csproj"
COPY . .
WORKDIR "/src/TestWeb"
RUN dotnet build "TestWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestWeb.dll"]