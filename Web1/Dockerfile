FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1803 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Web1/Web1.csproj Web1/
RUN dotnet restore Web1/Web1.csproj
COPY . .
WORKDIR /src/Web1
RUN dotnet build Web1.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Web1.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web1.dll"]