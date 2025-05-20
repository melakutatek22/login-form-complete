FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ./LoginForm.API/LoginForm.API.csproj ./LoginForm.API/
RUN dotnet restore ./LoginForm.API/LoginForm.API.csproj
COPY ./LoginForm.API ./LoginForm.API
WORKDIR /src/LoginForm.API
RUN dotnet build -c Release -o /app/build

FROM build AS publish
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LoginForm.API.dll"]
