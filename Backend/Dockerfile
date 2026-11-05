# Build with the SDK matching the existing net6.0 target framework.
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

COPY ["Backend.csproj", "./"]
RUN dotnet restore "Backend.csproj"

COPY . .
RUN dotnet publish "Backend.csproj" -c Release -o /app/publish /p:UseAppHost=false

# ASP.NET Core runtime for the existing .NET 6 application.
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS final
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080

COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Backend.dll"]
