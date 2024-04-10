# Deploy a containerized application to Cloud Run using Cloud Build

## Modified Cloud Build Quickstart

[https://cloud.google.com/build/docs/deploy-containerized-application-cloud-run](https://cloud.google.com/build/docs/deploy-containerized-application-cloud-run)

```bash

# Set environment variables
export PROJECT_ID=$(gcloud config get-value project)
export PROJECT_NUMBER="$(gcloud projects describe ${PROJECT_ID} --format='get(projectNumber)')"

export REGION=$(gcloud config get-value compute/region)
if [ "$REGION" = "(unset)" ] || [ -z "$REGION" ]; then
  export REGION="us-central1"
  gcloud config set compute/region $REGION
fi
echo "Region set to: $REGION"

export REPOSITORY=container

# Enable GCP Services used
gcloud services enable cloudbuild.googleapis.com artifactregistry.googleapis.com \
    run.googleapis.com eventarc.googleapis.com \
    logging.googleapis.com

# Grant the Cloud Run Admin role to the Cloud Build service account
gcloud projects add-iam-policy-binding ${PROJECT_ID} --member=serviceAccount:${PROJECT_NUMBER}@cloudbuild.gserviceaccount.com \
    --role=roles/run.admin

# Grant the IAM Service Account User role to the Cloud Build service account for the Cloud Run runtime service account
gcloud iam service-accounts add-iam-policy-binding \
    $PROJECT_NUMBER-compute@developer.gserviceaccount.com \
    --member=serviceAccount:$PROJECT_NUMBER@cloudbuild.gserviceaccount.com \
    --role=roles/iam.serviceAccountUser

# Use Cloud Build configuration file.
gcloud builds submit --config cloudbuild.yaml --substitutions=_REGION=us-west2

# Read up on Dynamic Variable Substitutions at:
# https://cloud.google.com/build/docs/configuring-builds/substitute-variable-values
