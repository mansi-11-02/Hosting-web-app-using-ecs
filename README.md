# Hosting-web-app-using-ecs

Push your java application image in ECR

1. Create cluster in ecs

   ![image](https://github.com/user-attachments/assets/89775fc2-48b8-4679-92d9-a65dd24379ec)

2. Create task definition : give task definition family name, container-name, image URI > create

   ![image](https://github.com/user-attachments/assets/ab3e1623-2f94-4b88-bc28-6a129126e720)

   ![image](https://github.com/user-attachments/assets/46f10ae7-89bf-42eb-8f57-7ee585dfc3df)

   or create using json file:

```yml
{
    "taskDefinitionArn": "arn:aws:ecs:ap-southeast-1:288761750357:task-definition/myapp-task:5",
    "containerDefinitions": [
        {
            "name": "my-webapp",
            "image": "288761750357.dkr.ecr.ap-southeast-1.amazonaws.com/mansi-28:latest",
            "cpu": 0,
            "portMappings": [
                {
                    "name": "my-webapp-80-tcp",
                    "containerPort": 80,
                    "hostPort": 80,
                    "protocol": "tcp",
                    "appProtocol": "http"
                }
            ],
            "essential": true,
            "environment": [],
            "environmentFiles": [],
            "mountPoints": [],
            "volumesFrom": [],
            "ulimits": [],
            "logConfiguration": {
                "logDriver": "awslogs",
                "options": {
                    "awslogs-group": "/ecs/myapp-task",
                    "mode": "non-blocking",
                    "awslogs-create-group": "true",
                    "max-buffer-size": "25m",
                    "awslogs-region": "ap-southeast-1",
                    "awslogs-stream-prefix": "ecs"
                },
                "secretOptions": []
            },
            "systemControls": []
        }
    ],
    "family": "myapp-task",
    "executionRoleArn": "arn:aws:iam::288761750357:role/ecsTaskExecutionRole",
    "networkMode": "awsvpc",
    "revision": 5,
    "volumes": [],
    "status": "ACTIVE",
    "requiresAttributes": [
        {
            "name": "com.amazonaws.ecs.capability.logging-driver.awslogs"
        },
        {
            "name": "ecs.capability.execution-role-awslogs"
        },
        {
            "name": "com.amazonaws.ecs.capability.ecr-auth"
        },
        {
            "name": "com.amazonaws.ecs.capability.docker-remote-api.1.19"
        },
        {
            "name": "com.amazonaws.ecs.capability.docker-remote-api.1.28"
        },
        {
            "name": "ecs.capability.execution-role-ecr-pull"
        },
        {
            "name": "com.amazonaws.ecs.capability.docker-remote-api.1.18"
        },
        {
            "name": "ecs.capability.task-eni"
        },
        {
            "name": "com.amazonaws.ecs.capability.docker-remote-api.1.29"
        }
    ],
    "placementConstraints": [],
    "compatibilities": [
        "EC2",
        "FARGATE"
    ],
    "requiresCompatibilities": [
        "FARGATE"
    ],
    "cpu": "1024",
    "memory": "3072",
    "runtimePlatform": {
        "cpuArchitecture": "X86_64",
        "operatingSystemFamily": "LINUX"
    },
    "registeredAt": "2024-09-29T18:17:54.531Z",
    "registeredBy": "arn:aws:iam::288761750357:root",
    "tags": []
}
```
3. Create a service : give service name, select security group who has allowed 8080 port

   ![image](https://github.com/user-attachments/assets/f4de8117-1aa9-40b5-b494-1201951f0c59)


4. Task will be created automatically

   ![image](https://github.com/user-attachments/assets/4250bfcf-3ee2-47c6-999b-96ca74e8d60c)

5. Copy the public ip of the task and run it in the browser: http://ip-address:8080/webapp






