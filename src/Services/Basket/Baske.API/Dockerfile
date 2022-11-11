#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Services/Basket/Baske.API/Baske.API.csproj", "Services/Basket/Baske.API/"]
RUN dotnet restore "Services/Basket/Baske.API/Baske.API.csproj"
COPY . .
WORKDIR "/src/Services/Basket/Baske.API"
RUN dotnet build "Baske.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Baske.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Baske.API.dll"]
