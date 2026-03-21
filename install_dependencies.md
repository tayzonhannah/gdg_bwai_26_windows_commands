Instead of:

```
source .env
```

Do this isntead:

```
if (Test-Path .env) {
    Get-Content .env | ForEach-Object {
        # Skip empty lines and comments
        if (![string]::IsNullOrWhiteSpace($_) -and !($_.StartsWith('#'))) {
            $name, $value = $_ -split '=', 2
            
            # Clean up the strings and set the environment variable
            $cleanName = $name.Trim()
            $cleanValue = $value.Trim(" `"'")
            Set-Item -Path Env:\$cleanName -Value $cleanValue
            
            Write-Host "✅ Loaded: $cleanName" -ForegroundColor Green
        }
    }
} else {
    Write-Host "❌ .env file not found in this directory!" -ForegroundColor Red
}
```

Instead of:

```
cat > restaurant_concierge/.env <<EOF
GOOGLE_CLOUD_PROJECT=${GOOGLE_CLOUD_PROJECT}
GOOGLE_CLOUD_LOCATION=global
GOOGLE_GENAI_USE_VERTEXAI=True
EOF
```

Do this:

```
# 1. Grab the correct project ID directly from gcloud
$projectId = gcloud config get-value project

# 2. Build the contents of the new .env file
$envLines = @(
    "GOOGLE_CLOUD_PROJECT=$projectId",
    "GOOGLE_CLOUD_LOCATION=global",
    "GOOGLE_GENAI_USE_VERTEXAI=True"
)

# 3. Write it to the restaurant_concierge folder
Set-Content -Path "restaurant_concierge\.env" -Value $envLines

# 4. Print it out to verify it worked perfectly
Write-Host "✅ Created restaurant_concierge\.env with contents:`n" -ForegroundColor Green
Get-Content "restaurant_concierge\.env"
```

