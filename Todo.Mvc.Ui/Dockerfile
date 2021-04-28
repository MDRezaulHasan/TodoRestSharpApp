#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM microsoft/aspnetcore:2.0-stretch AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-stretch AS build
WORKDIR /src
COPY ["Todo.Mvc.Ui/Todo.Mvc.Ui.csproj", "Todo.Mvc.Ui/"]
COPY ["../../RestSharpTodo/RestSharpTodo.csproj", "../../RestSharpTodo/"]
RUN dotnet restore "Todo.Mvc.Ui/Todo.Mvc.Ui.csproj"
COPY . .
WORKDIR "/src/Todo.Mvc.Ui"
RUN dotnet build "Todo.Mvc.Ui.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Todo.Mvc.Ui.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Todo.Mvc.Ui.dll"]