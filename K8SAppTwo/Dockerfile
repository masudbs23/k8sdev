FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["K8SAppTwo/K8SAppTwo.csproj", "K8SAppTwo/"]
RUN dotnet restore "K8SAppTwo/K8SAppTwo.csproj"
COPY . .
WORKDIR "/src/K8SAppTwo"
RUN dotnet build "K8SAppTwo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "K8SAppTwo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "K8SAppTwo.dll"]