FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["PipelineDemo.Email/PipelineDemo.Email.csproj", "PipelineDemo.Email/"]
RUN dotnet restore "PipelineDemo.Email/PipelineDemo.Email.csproj"
COPY . .
WORKDIR "/src/PipelineDemo.Email"
RUN dotnet build "PipelineDemo.Email.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PipelineDemo.Email.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PipelineDemo.Email.dll"]
