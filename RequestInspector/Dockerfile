FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY RequestInspector/RequestInspector.csproj RequestInspector/
RUN dotnet restore RequestInspector/RequestInspector.csproj
COPY . .
WORKDIR /src/RequestInspector
RUN dotnet build RequestInspector.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish RequestInspector.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RequestInspector.dll"]
