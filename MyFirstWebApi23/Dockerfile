#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MyFirstWebApi23/MyFirstWebApi23.csproj", "MyFirstWebApi23/"]
RUN dotnet restore "MyFirstWebApi23/MyFirstWebApi23.csproj"
COPY . .
WORKDIR "/src/MyFirstWebApi23"
RUN dotnet build "MyFirstWebApi23.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyFirstWebApi23.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyFirstWebApi23.dll"]