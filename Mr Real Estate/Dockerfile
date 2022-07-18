#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Mr Real Estate/Mr Real Estate.csproj", "Mr Real Estate/"]
RUN dotnet restore "Mr Real Estate/Mr Real Estate.csproj"
COPY . .
WORKDIR "/src/Mr Real Estate"
RUN dotnet build "Mr Real Estate.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Mr Real Estate.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Mr Real Estate.dll"]