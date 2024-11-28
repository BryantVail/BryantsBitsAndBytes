#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BryantsBitsAndBytes_mvc/BryantsBitsAndBytes_mvc.csproj", "BryantsBitsAndBytes_mvc/"]
RUN dotnet restore "BryantsBitsAndBytes_mvc/BryantsBitsAndBytes_mvc.csproj"
COPY . .
WORKDIR "/src/BryantsBitsAndBytes_mvc"
RUN dotnet build "BryantsBitsAndBytes_mvc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BryantsBitsAndBytes_mvc.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BryantsBitsAndBytes_mvc.dll"]