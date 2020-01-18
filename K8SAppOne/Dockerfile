FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["K8SAppOne/K8SAppOne.csproj", "K8SAppOne/"]
RUN dotnet restore "K8SAppOne/K8SAppOne.csproj"
COPY . .
WORKDIR "/src/K8SAppOne"
RUN dotnet build "K8SAppOne.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "K8SAppOne.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "K8SAppOne.dll"]