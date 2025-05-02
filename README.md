# soap-sample-dotnetcore
Sample project for showing .NET Core Soap endpoint


Initial setup achieved in codespaces using these commands

```bash
# Pick a name for your repo / solution
export APP_NAME=WeatherService

# Create workspace and go inside it
mkdir $APP_NAME && cd $_

# Create a solution container, then a Web API project targeting .NET 9
dotnet new sln -n $APP_NAME
dotnet new webapi -n $APP_NAME.Api -f net9.0

# Add the project to the solution
dotnet sln add $APP_NAME.Api/$APP_NAME.Api.csproj


```

And then modified default codespace container using this

```bash
mkdir .devcontainer
cat > .devcontainer/devcontainer.json <<'EOF'
{
  "name": ".NET 9 Codespace",
  "image": "mcr.microsoft.com/devcontainers/dotnet:9.0",  // Microsoft‑maintained image with SDK 9
  "features": {
    "ghcr.io/devcontainers/features/git:1": {}
  },
  // Optional: forward common ports
  "forwardPorts": [5000, 5001]
}
EOF

# Commit the devcontainer so Codespaces picks it up
git add .devcontainer/devcontainer.json
git commit -m "Add .devcontainer for Codespaces"
git push


```

Run application using 

```bash
dotnet restore
dotnet build
dotnet run --project WeatherService.Api

```