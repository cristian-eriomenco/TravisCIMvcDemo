FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 54764
EXPOSE 44386

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TravisCIMvcDemo/TravisCIMvcDemo.csproj", "TravisCIMvcDemo/"]
RUN dotnet restore "TravisCIMvcDemo/TravisCIMvcDemo.csproj"
COPY . .
WORKDIR "/src/TravisCIMvcDemo"
RUN dotnet build "TravisCIMvcDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TravisCIMvcDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TravisCIMvcDemo.dll"]