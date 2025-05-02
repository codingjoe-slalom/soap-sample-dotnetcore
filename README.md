# soap-sample-dotnetcore
Sample project for showing .NET Core Soap endpoint


Initial setup achieved in codespaces using these commands

```bash
mkdir .devcontainer
cat > .devcontainer/devcontainer.json <<'EOF'
{
  "name": ".NET 9 Codespace",
  "image": "mcr.microsoft.com/devcontainers/dotnet:9.0",  
  "features": {
    "ghcr.io/devcontainers/features/git:1": {}
  },
  "containerEnv": {
    "ASPNETCORE_URLS": "https://+:5001;http://+:5000",
    "ASPNETCORE_HTTPS_PORT": "5001"
  },
  "forwardPorts": [5000, 5001]
}
EOF

# Create self-signed cert
dotnet dev-certs https --trust

# Commit the devcontainer so Codespaces picks it up
git add .devcontainer/devcontainer.json
git commit -m "Add .devcontainer for Codespaces"
git add .
git commit -m "Setup starter code"
git push
# Rebuild the full codespace
gh codespace rebuild --full

```

And then create dotnet 9.0 project

```bash
# Pick a name for your repo / solution
export APP_NAME=WeatherService

# Create a solution container, then a Web API project targeting .NET 9
dotnet new sln -n $APP_NAME
dotnet new webapi -n $APP_NAME.Api -f net9.0

# Add the project to the solution
dotnet sln add $APP_NAME.Api/$APP_NAME.Api.csproj


```


Run application using 

```bash
dotnet restore
dotnet build
dotnet run --project WeatherService.Api

```