# Automate builds by using Cloud Build

## Modified Cloud Build Quickstart

- Official Cloud Build examples [https://github.com/GoogleCloudPlatform/cloud-build-samples/tree/main/quickstart-automate](https://github.com/GoogleCloudPlatform/cloud-build-samples/tree/main/quickstart-automate)
- Fork and clone above GCP repo (or this one [https://github.com/dzivkovi/hello-cloud-build](https://github.com/dzivkovi/hello-cloud-build))
- Follow the instructions in [https://cloud.google.com/build/docs/automate-builds](https://cloud.google.com/build/docs/automate-builds)

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

export REPOSITORY=quickstart
