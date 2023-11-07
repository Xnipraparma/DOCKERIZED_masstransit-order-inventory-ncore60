FROM mcr.microsoft.com/dotnet/sdk:6.0 AS base
WORKDIR /invapp

EXPOSE 80
EXPOSE 5054

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY . .

COPY . .
WORKDIR "/src/."
RUN dotnet build "InventoryService/InventoryService.csproj" -c Release -o /invapp

FROM build AS publish
RUN dotnet publish "InventoryService/InventoryService.csproj" -c Release -o /invapp

FROM base AS final
WORKDIR /invapp
COPY --from=publish /invapp .
ENTRYPOINT ["dotnet", "InventoryService/InventoryService.dll", "--server.urls", "http://0.0.0.0:5054"]