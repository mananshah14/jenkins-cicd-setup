# Application

This is a two-tier application.

<img width="353" alt="HLD-2-Tier_application" src="https://github.com/mananshah14/jenkins-cicd-setup/assets/45019538/0a3b6c10-556b-472e-8590-a6194e22608e">



## Getting Started

To get started with this project, follow these steps:


1. Clone the repository.
2. Make sure the backend server is running (see instructions below).

## Usage

- Click the "Send Request" button to interact with the backend.
- View the response received from the backend.

## Configuration

You can configure the backend URL by updating the `backendUrl` variable in `config.json`. This file can be found at the root of the project.

```json
{
  "backendUrl": "http://127.0.0.1:5000"
}
```

Update the backendUrl value to match the URL of your backend server.

## Running the Backend
To run the backend server, follow these steps:

pre-requisites: `python 3.11`

1. Navigate to the backend directory.
2. Build the Image using the given DockerFile.
3. Run the Backend server by running.
   
```
docker-compose up -d
```
