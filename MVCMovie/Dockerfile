FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["MVCMovie/MVCMovie.csproj", "MVCMovie/"]

RUN dotnet restore "MVCMovie/MVCMovie.csproj"
COPY . .
WORKDIR "/src/MVCMovie"
RUN dotnet build "MVCMovie.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MVCMovie.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MVCMovie.dll"]