FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
EXPOSE 1232
EXPOSE 1231
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY APIGW.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "APIGW.dll"]