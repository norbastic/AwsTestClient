FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AwsTestClient/AwsTestClient.csproj", "AwsTestClient/"]
RUN dotnet restore "AwsTestClient/AwsTestClient.csproj"
COPY . .
WORKDIR "/src/AwsTestClient"
RUN dotnet build "AwsTestClient.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AwsTestClient.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AwsTestClient.dll"]
