FROM mcr.microsoft.com/dotnet/sdk:5.0 AS publish

RUN mkdir /app
RUN mkdir /app/out

WORKDIR /app
COPY . ./

RUN dotnet publish        \
  --configuration debug \
  --output out       \
  www.csproj

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS deploy

RUN mkdir /src
RUN mkdir /app
WORKDIR /app

COPY --from=publish /app /src
COPY --from=publish /app/out /app

CMD [ "dotnet", "/app/www.dll" ]