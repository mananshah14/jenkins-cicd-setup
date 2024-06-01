## Running the Backend
To run the backend server, follow these steps:

1. Navigate to the backend directory.
2. Run the Jenkinsfile in the jenkins server which Build, Test and Deploy the entire backend.

#### Local Testing:
1. Create the Image using the present Dockerfile
   
```
docker build -t backend .
```

2. Run the Backend Server using the below command

```
docker-compose up -d
```

Once your backend is up and running, you can proceed with setting up of frontend, Do Ensure to make the below configuration  before setting up th frontend

## Configuration

You can configure the backend URL by updating the `backendUrl` variable in `config.json`. This file can be found in the frontend/src directory.

```json
{
  "backendUrl": "http://127.0.0.1:5000"
}
```

Update the backendUrl value to match the URL of your backend server.

