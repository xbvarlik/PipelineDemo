FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["PipelineDemo.Product/PipelineDemo.Product.csproj", "PipelineDemo.Product/"]
RUN dotnet restore "PipelineDemo.Product/PipelineDemo.Product.csproj"
COPY . .
WORKDIR "/src/PipelineDemo.Product"
RUN dotnet build "PipelineDemo.Product.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PipelineDemo.Product.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PipelineDemo.Product.dll"]
