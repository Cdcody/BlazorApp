FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /chatApp

EXPOSE 8080
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BlazorChatApp.csproj", "."]
RUN dotnet restore "BlazorChatApp.csproj"
COPY . .
RUN dotnet build "BlazorChatApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorChatApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /chatApp
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorChatApp.dll"]