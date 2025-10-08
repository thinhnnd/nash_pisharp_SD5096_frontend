# Nash PiSharp Frontend

## Overview

Nash PiSharp Frontend is a React.js application that provides the user interface for the Nash PiSharp project.

## CI/CD Pipeline

This repository includes Azure DevOps Pipeline configuration for automated build and deployment.

### Pipeline Configuration

- **File**: `azure-pipelines.yml`
- **Triggers**: Automatically triggered on `main` and `develop` branch changes
- **Registry**: Azure Container Registry (ACR)
- **Image Repository**: `frontend`

### Version Management

Version is managed through `version.json` file:
```json
{
  "major": 1,
  "minor": 0,
  "description": "Nash PiSharp Frontend Application"
}
```

### Image Tags

- **Main branch**: `v{major}.{minor}.{buildId}` and `latest`
- **Develop branch**: `v{major}.{minor}.{buildId}` and `dev-v{major}.{minor}.{buildId}`
- **Other branches**: `v{major}.{minor}.{buildId}` only

### Setup Pipeline

1. Create a new pipeline in Azure DevOps
2. Connect to this repository
3. Use the existing `azure-pipelines.yml` file
4. Configure the following variables:
   - `containerRegistry`: Your ACR service connection name
   - Update ACR service connection if needed

## Docker Configuration

#### Snippet of frontend(ReactJS)`DockerFile`

You will find this `DockerFile` inside **frontend** directory. 

```bash
# Create image based on the official Node image from dockerhub
FROM node:10
#Argument that is passed from docer-compose.yaml file
ARG FRONT_END_PORT
# Create app directory
WORKDIR /usr/src/app
#Echo the argument to check passed argument loaded here correctly
RUN echo "Argument port is : $FRONT_END_PORT"
# Copy dependency definitions
COPY package.json /usr/src/app
# Install dependecies
RUN npm install
# Get all the code needed to run the app
COPY . /usr/src/app
# Expose the port the app runs in
EXPOSE ${FRONT_END_PORT}
# Serve the app
CMD ["npm", "start"]
```
##### Explanation of frontend(ReactJS) `DockerFile`

Frontend `DockerFile` is almost the same as Backend `DockerFile`.
