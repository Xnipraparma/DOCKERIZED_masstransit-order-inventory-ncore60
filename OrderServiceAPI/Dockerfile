FROM mcr.microsoft.com/dotnet/sdk:6.0 AS base
WORKDIR /app

EXPOSE 80
EXPOSE 5024

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY . .

COPY . .
WORKDIR "/src/."
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .

ENTRYPOINT ["dotnet", "OrderService.dll", "--server.urls", "http://0.0.0.0:5024"]