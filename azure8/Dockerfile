#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["azure8/azure8.csproj", "azure8/"]
RUN dotnet restore "azure8/azure8.csproj"
COPY . .
WORKDIR "/src/azure8"
RUN dotnet build "azure8.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "azure8.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "azure8.dll"]