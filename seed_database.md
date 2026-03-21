```
source.env
```


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
