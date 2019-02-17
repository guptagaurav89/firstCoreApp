FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["firstCoreApp/firstCoreApp.csproj", "firstCoreApp/"]
RUN dotnet restore "firstCoreApp/firstCoreApp.csproj"
COPY . .
WORKDIR "/src/firstCoreApp"
RUN dotnet build "firstCoreApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "firstCoreApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "firstCoreApp.dll"]