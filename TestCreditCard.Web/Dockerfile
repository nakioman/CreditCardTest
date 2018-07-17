FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 52902
EXPOSE 44326

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY TestCreditCard.Web/TestCreditCard.Web.csproj TestCreditCard.Web/
RUN dotnet restore TestCreditCard.Web/TestCreditCard.Web.csproj
COPY . .
WORKDIR /src/TestCreditCard.Web
RUN dotnet build TestCreditCard.Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TestCreditCard.Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestCreditCard.Web.dll"]
