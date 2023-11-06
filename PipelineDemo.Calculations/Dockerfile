FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["PipelineDemo.Calculations/PipelineDemo.Calculations.csproj", "PipelineDemo.Calculations/"]
RUN dotnet restore "PipelineDemo.Calculations/PipelineDemo.Calculations.csproj"
COPY . .
WORKDIR "/src/PipelineDemo.Calculations"
RUN dotnet build "PipelineDemo.Calculations.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PipelineDemo.Calculations.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PipelineDemo.Calculations.dll"]
