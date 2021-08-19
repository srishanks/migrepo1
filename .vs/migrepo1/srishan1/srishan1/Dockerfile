FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["srishan1/srishan1.csproj", "srishan1/"]
RUN dotnet restore "srishan1/srishan1.csproj"
COPY . .
WORKDIR "/src/srishan1"
RUN dotnet build "srishan1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "srishan1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "srishan1.dll"]