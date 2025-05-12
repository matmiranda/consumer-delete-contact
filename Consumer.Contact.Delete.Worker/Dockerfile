FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["Consumer.Contact.Delete.Worker/Consumer.Contact.Delete.ApWorkeri.csproj", "Consumer.Contact.Delete.Worker/"]
COPY ["Consumer.Contact.Delete.Domain/Consumer.Contact.Delete.Domain.csproj", "Consumer.Contact.Delete.Domain/"]
COPY ["Consumer.Contact.Delete.Infrastructure/Consumer.Contact.Delete.Infrastructure.csproj", "Consumer.Contact.Delete.Infrastructure/"]
COPY ["Consumer.Contact.Delete.Application/Consumer.Contact.Delete.Application.csproj", "Consumer.Contact.Delete.Application/"]
RUN dotnet restore "Consumer.Contact.Delete.Worker/Consumer.Contact.Delete.Worker.csproj"
COPY . .
WORKDIR "/src/Consumer.Contact.Delete.Worker"
RUN dotnet build -c Release -o /app/build
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:80
ENTRYPOINT ["dotnet", "Consumer.Contact.Delete.Worker.dll"]
