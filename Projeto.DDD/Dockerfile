FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Projeto.DDD/Projeto.DDD.csproj", "Projeto.DDD/"]
RUN dotnet restore "Projeto.DDD/Projeto.DDD.csproj"
COPY . .
WORKDIR "/src/Projeto.DDD"
RUN dotnet build "Projeto.DDD.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Projeto.DDD.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Projeto.DDD.dll"]