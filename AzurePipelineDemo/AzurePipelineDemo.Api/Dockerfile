#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["AzurePipelineDemo.Api/AzurePipelineDemo.Api.csproj", "AzurePipelineDemo.Api/"]
RUN dotnet restore "AzurePipelineDemo.Api/AzurePipelineDemo.Api.csproj"
COPY . .
WORKDIR "/src/AzurePipelineDemo.Api"
RUN dotnet build "AzurePipelineDemo.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AzurePipelineDemo.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AzurePipelineDemo.Api.dll"]