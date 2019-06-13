FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["SherlockAvlApI/SherlockAvlApI.csproj", "SherlockAvlApI/"]
RUN dotnet restore "SherlockAvlApI/SherlockAvlApI.csproj"
COPY . .
WORKDIR "/src/SherlockAvlApI"
RUN dotnet build "SherlockAvlApI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SherlockAvlApI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SherlockAvlApI.dll"]