# Build and push a Docker image with Cloud Build

## Modified Cloud Build Quickstart

[https://cloud.google.com/build/docs/build-push-docker-image](https://cloud.google.com/build/docs/build-push-docker-image)


```bash

# GCP Project context
export PROJECT_ID=$(gcloud config get-value project)
export PROJECT_NUMBER="$(gcloud projects describe ${PROJECT_ID} --format='get(projectNumber)')"

export REGION=$(gcloud config get-value compute/region)
if [ "$REGION" = "(unset)" ] || [ -z "$REGION" ]; then
  export REGION="us-central1"
  gcloud config set compute/region $REGION
fi
echo "Region set to: $REGION"


# Atrifact Registry setup
gcloud services enable cloudbuild.googleapis.com artifactregistry.googleapis.com \
    run.googleapis.com eventarc.googleapis.com \
    logging.googleapis.com

gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUMBER}@cloudbuild.gserviceaccount.com \
    --role=roles/artifactregistry.writer

export REPOSITORY=quickstart
gcloud artifacts repositories create $REPOSITORY --repository-format=docker --location=$REGION --description="Docker repo"

# Cloud Build setup
gcloud builds submit --region=$REGION --tag $REGION-docker.pkg.dev/$PROJECT_ID/$REPOSITORY/quickstart-image:tag1

# Validate the image
gcloud artifacts docker images list $REGION-docker.pkg.dev/$PROJECT_ID/$REPOSITORY --include-tags

# Script to deploy the image
