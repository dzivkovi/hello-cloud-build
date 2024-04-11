# Automate builds by using Cloud Build

## Read-along Quickstart

- Official Cloud Build examples [https://github.com/GoogleCloudPlatform/cloud-build-samples/tree/main/quickstart-automate](https://github.com/GoogleCloudPlatform/cloud-build-samples/tree/main/quickstart-automate)
- Fork and clone above GCP repo (or this one [https://github.com/dzivkovi/hello-cloud-build](https://github.com/dzivkovi/hello-cloud-build))
- Follow the instructions in [https://cloud.google.com/build/docs/automate-builds](https://cloud.google.com/build/docs/automate-builds)

## Post-Quickstart Steps

- Identifying Trigger ID

  ```bash
  gcloud builds triggers list
  ```

  In the output, each trigger block ends with an `id` field which uniquely identifies the trigger. e.g. `id: d51e16de-293e-4203-b6db-27bad1f70395`

- Exporting Trigger Configuration

  ```bash
  gcloud builds triggers describe d51e16de-293e-4203-b6db-27bad1f70395 --format=json
  ```

## Advanced Tutorial

- Cloud Run Canary Deployments: [https://www.cloudskillsboost.google/course_templates/691/labs/452141](https://www.cloudskillsboost.google/course_templates/691/labs/452141)
- Code behind the Qwiklab: [Canary Deployments with Cloud Run and Cloud Build](https://github.com/GoogleCloudPlatform/software-delivery-workshop/tree/main/labs/cloudrun-progression)
