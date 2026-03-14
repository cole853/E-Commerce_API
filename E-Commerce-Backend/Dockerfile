FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

USER app
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG configuration=Release
WORKDIR /src
COPY ["E-Commerce-Backend/E-Commerce-Backend.csproj", "E-Commerce-Backend/"]
RUN dotnet restore "E-Commerce-Backend/E-Commerce-Backend.csproj"
COPY . .
WORKDIR "/src/E-Commerce-Backend"
RUN dotnet build "E-Commerce-Backend.csproj" -c $configuration -o /app/build

FROM build AS publish
ARG configuration=Release
RUN dotnet publish "E-Commerce-Backend.csproj" -c $configuration -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "E-Commerce-Backend.dll"]
