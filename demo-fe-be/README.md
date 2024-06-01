#  2 Tier Application  using FLask and NodeJS

This is a two-tier application.

 #### 2 Tier Application Deployment Approach (HLD)

<img width="500" alt="HLD-2-Tier_application" src="https://github.com/mananshah14/jenkins-cicd-setup/assets/45019538/0a3b6c10-556b-472e-8590-a6194e22608e">


#### 2 Tier Application Deployment Approach (LLD)

![image](https://github.com/mananshah14/jenkins-cicd-setup/assets/45019538/2cb3e9d6-759d-448c-8949-4e3db924c338)


## Getting Started

To get started with this project, follow these steps:


1. Clone the repository.
2. Make sure the backend server is running (see instructions below).

## Usage

- Click the "Send Request" button to interact with the backend.
- View the response received from the backend.


## Running the Backend
To run the backend server, follow these steps:

1. Navigate to the backend directory.
2. Build the Image using the given DockerFile.
3. Run the Backend server by running.

               OR

Run the Jenkinsfile in the jenkins server which Build, Test and Deploy the entire backend. 
   
```
docker-compose up -d
```

Once your backend is up and running, can proceed with setting up of frontend, Do Ensure to make the below configuration  before setting up th frontend

## Configuration

You can configure the backend URL by updating the `backendUrl` variable in `config.json`. This file can be found in the frontend/src directory.

```json
{
  "backendUrl": "http://127.0.0.1:5000"
}
```

Update the backendUrl value to match the URL of your backend server.
