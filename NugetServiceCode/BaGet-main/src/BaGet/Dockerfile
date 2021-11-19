#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["nuget.config", "."]
COPY ["src/BaGet/BaGet.csproj", "src/BaGet/"]
COPY ["src/BaGet.Core/BaGet.Core.csproj", "src/BaGet.Core/"]
COPY ["src/BaGet.Protocol/BaGet.Protocol.csproj", "src/BaGet.Protocol/"]
COPY ["src/BaGet.Database.Sqlite/BaGet.Database.Sqlite.csproj", "src/BaGet.Database.Sqlite/"]
COPY ["src/BaGet.Database.SqlServer/BaGet.Database.SqlServer.csproj", "src/BaGet.Database.SqlServer/"]
COPY ["src/BaGet.Aliyun/BaGet.Aliyun.csproj", "src/BaGet.Aliyun/"]
COPY ["src/BaGet.Database.PostgreSql/BaGet.Database.PostgreSql.csproj", "src/BaGet.Database.PostgreSql/"]
COPY ["src/BaGet.Gcp/BaGet.Gcp.csproj", "src/BaGet.Gcp/"]
COPY ["src/BaGet.Database.MySql/BaGet.Database.MySql.csproj", "src/BaGet.Database.MySql/"]
COPY ["src/BaGet.Aws/BaGet.Aws.csproj", "src/BaGet.Aws/"]
COPY ["src/BaGet.Web/BaGet.Web.csproj", "src/BaGet.Web/"]
COPY ["src/BaGet.Azure/BaGet.Azure.csproj", "src/BaGet.Azure/"]
RUN dotnet restore "src/BaGet/BaGet.csproj"
COPY . .
WORKDIR "/src/src/BaGet"
RUN dotnet build "BaGet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BaGet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BaGet.dll"]
