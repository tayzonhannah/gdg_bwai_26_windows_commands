
--for when *bash setup_verify_trial_project.sh && source .env* doesn't work

```
if (Test-Path .env) {
    Get-Content .env | ForEach-Object {
        # Ignore empty lines and comments
        if (![string]::IsNullOrWhiteSpace($_) -and !($_.StartsWith('#'))) {
            $name, $value = $_ -split '=', 2
            # Clean up whitespace and quotes
            $name = $name.Trim()
            $value = $value.Trim(" `"'")
            
            # Set the environment variable
            Set-Item -Path Env:\$name -Value $value
            Write-Host "✅ Loaded: $name" -ForegroundColor Green
        }
    }
} else {
    Write-Host "❌ .env file not found!" -ForegroundColor Red
}
```
