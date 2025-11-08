# BillingSystem.Web/Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["BillingSystem.Web/BillingSystem.Web.csproj", "BillingSystem.Web/"]
COPY ["BillingSystem.Application/BillingSystem.Application.csproj", "BillingSystem.Application/"]
COPY ["BillingSystem.Domain/BillingSystem.Domain.csproj", "BillingSystem.Domain/"]
COPY ["BillingSystem.Infrastructure/BillingSystem.Infrastructure.csproj", "BillingSystem.Infrastructure/"]
RUN dotnet restore "BillingSystem.Web/BillingSystem.Web.csproj"

COPY . .
WORKDIR /src/BillingSystem.Web
RUN dotnet publish -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:5000
EXPOSE 5000
ENTRYPOINT ["dotnet", "BillingSystem.Web.dll"]
