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
# 1. Fetch the service account and save it to a PowerShell variable
$SERVICE_ACCOUNT = (gcloud sql instances describe restaurant-db --format="value(serviceAccountEmailAddress)")

# Print it out to verify we actually grabbed it
Write-Host "✅ Found Service Account: $SERVICE_ACCOUNT" -ForegroundColor Green

# 2. Apply the IAM policy using the variable and your active project
gcloud projects add-iam-policy-binding (gcloud config get-value project) `
   --member="serviceAccount:$SERVICE_ACCOUNT" `
   --role="roles/aiplatform.user" `
   --quiet
```
