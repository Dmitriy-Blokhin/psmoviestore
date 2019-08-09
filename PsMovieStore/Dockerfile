FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["PsMovieStore/PsMovieStore.csproj", "PsMovieStore/"]
RUN dotnet restore "PsMovieStore/PsMovieStore.csproj"
COPY . .
WORKDIR "/src/PsMovieStore"
RUN dotnet build "PsMovieStore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PsMovieStore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PsMovieStore.dll"]
