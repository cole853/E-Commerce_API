# Written by DeepSeek
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy solution file if it exists
COPY ["E-Commerce_API.sln", "."]
# Copy project files with their relative paths
COPY ["E-Commerce-Backend/E-Commerce-Backend.csproj", "E-Commerce-Backend/"]
COPY ["E-Commerce-Backend.Tests/E-Commerce-Backend.Tests.csproj", "E-Commerce-Backend.Tests/"]

# Restore using solution file (if available) or individual projects
RUN dotnet restore "E-Commerce_API.sln" || \
    (dotnet restore "E-Commerce-Backend/E-Commerce-Backend.csproj" && \
     dotnet restore "E-Commerce-Backend.Tests/E-Commerce-Backend.Tests.csproj")

# Copy everything
COPY . .

# Build and run tests
WORKDIR "/src/E-Commerce-Backend.Tests"
RUN dotnet build "E-Commerce-Backend.Tests.csproj" -c Release --no-restore
ENTRYPOINT ["dotnet", "test", "--logger:trx", "--results-directory", "/test-results"]