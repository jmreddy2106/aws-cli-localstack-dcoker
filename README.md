# AWS Cloud Computing

## AWS CLI + LocalStack (Local Docker Environment)

### Install Required Tools
#### Install Docker Desktop https://www.docker.com/products/docker-desktop

## Verify Docker
```bash 
    docker --version
```
## Install LocalStack CLI
```bash 
    pip install localstack
```

## Install AWS CLI v2 https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
```bash 
    aws --version`
```

## Install awslocal (wrapper for LocalStack)
```bash 
    pip install awscli-local
```


## Run the docker compose

## Configure AWS CLI for LocalStack

```bash 
    aws configure
```
```bash
    AWS Access Key ID: test
    AWS Secret Access Key: test
    Default region: us-east-1
    Default output format: json
```
Add to ~/.aws/config:
```bash
    [profile localstack]
    region = us-east-1
    output = json
    endpoint_url = http://localhost:4566
```

Note: All commands use `awslocal` (auto-points to LocalStack) OR `aws --endpoint-url=http://localhost:4566` interchangeably.


# Run docekr compose file
```bash
    docker-compose up -d
```

# Verify all services are running
```bash
    curl http://localhost:4566/_localstack/health 
```


