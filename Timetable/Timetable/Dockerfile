FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Timetable/Timetable.csproj", "Timetable/"]
RUN dotnet restore "Timetable/Timetable.csproj"
COPY . .
WORKDIR "/src/Timetable"
RUN dotnet build "Timetable.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Timetable.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .

CMD ASPNETCORE_URLS=http://*:$PORT dotnet Timetable.dll