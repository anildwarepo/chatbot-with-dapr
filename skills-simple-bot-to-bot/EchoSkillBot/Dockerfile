#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 39783
ENV ASPNETCORE_URLS=http://*:39783

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["EchoSkillBot.csproj", ""]
RUN dotnet restore "./EchoSkillBot.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "EchoSkillBot.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EchoSkillBot.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Microsoft.BotBuilderSamples.EchoSkillBot.dll"]