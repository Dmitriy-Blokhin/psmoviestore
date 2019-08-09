FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["PsPricingApi/PsPricingApi.csproj", "PsPricingApi/"]
RUN dotnet restore "PsPricingApi/PsPricingApi.csproj"
COPY . .
WORKDIR "/src/PsPricingApi"
RUN dotnet build "PsPricingApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PsPricingApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PsPricingApi.dll"]
