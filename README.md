# Setup

## environment

```bash
export PROJECT_ID=`gcloud config list --format 'value(core.project)'`
export SLACK_BOT_TOKEN=
export SLACK_APP_TOKEN=
export APP_ENVIRONMENT=prod
export SLACK_SIGNING_SECRET=
```

## docker

```bash
gcp_project=`gcloud config list --format 'value(core.project)'`
image_name=gemini-stg
gcloud auth login
gcloud config set project $gcp_project

gcloud auth configure-docker asia-northeast1-docker.pkg.dev
gcloud artifacts repositories create $image_name --location=asia-northeast1 --repository-format=docker --project=$gcp_project

docker rmi asia-northeast1-docker.pkg.dev/$gcp_project/$image_name/$image_name && docker rmi $image_name
docker build . -t $image_name --platform linux/amd64
docker tag $image_name asia-northeast1-docker.pkg.dev/$gcp_project/$image_name/$image_name && docker push asia-northeast1-docker.pkg.dev/$gcp_project/$image_name/$image_name:latest
```
