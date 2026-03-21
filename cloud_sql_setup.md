Instead of this:

```
SERVICE_ACCOUNT=$(gcloud sql instances describe restaurant-db --format="value(serviceAccountEmailAddress)")

gcloud projects add-iam-policy-binding $GOOGLE_CLOUD_PROJECT \
  --member="serviceAccount:$SERVICE_ACCOUNT" \
  --role="roles/aiplatform.user" \
  --quiet

```

Do this:
```
$SERVICE_ACCOUNT = (gcloud sql instances describe restaurant-db --format="value(serviceAccountEmailAddress)")

gcloud projects add-iam-policy-binding (gcloud config get-value project) `
   --member="serviceAccount:$SERVICE_ACCOUNT" `
   --role="roles/aiplatform.user" `
   --quiet
```
