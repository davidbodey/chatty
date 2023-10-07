FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["ChatWebApp/ChatWebApp.csproj", "ChatWebApp/"]
RUN dotnet restore "ChatWebApp/ChatWebApp.csproj"
COPY . .
WORKDIR "/src/ChatWebApp"
RUN dotnet build "ChatWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ChatWebApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ChatWebApp.dll"]
