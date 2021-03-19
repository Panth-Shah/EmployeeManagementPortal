#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["EmployeeManagementPortal/EmployeeManagementPortal.csproj", "EmployeeManagementPortal/"]
RUN dotnet restore "EmployeeManagementPortal/EmployeeManagementPortal.csproj"
COPY . .
WORKDIR "/src/EmployeeManagementPortal"
RUN dotnet build "EmployeeManagementPortal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EmployeeManagementPortal.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EmployeeManagementPortal.dll"]