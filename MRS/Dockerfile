FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MRS/MRS.csproj", "MRS/"]
RUN dotnet restore "MRS/MRS.csproj"
COPY . .
WORKDIR "/src/MRS"
RUN dotnet build "MRS.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MRS.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MRS.dll"]
