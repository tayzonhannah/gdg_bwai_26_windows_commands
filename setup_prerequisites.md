#### COPY PASTE THIS INTO THE TERMINAL; DO IT ONE BY ONE

# 1. Git
-- to check if it's already installed

```git --version```


-- to install

```winget install --id Git.Git -e --source winget```

# 2. Curl

-- this should be installed in your system already. To check use the following command:

```curl.exe --version ```

# 3. UV - Python Package Manager

--to check its version

```uv --version```

--to install

```powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"```

# 4. Python 3.12

--check if you have python 3.12 already

```uv python find 3.12```

-- to install 

```uv python install 3.12```

# 5. Google Cloud (gcloud) CLI

```gcloud version```

```
$gcloudInstaller = "$env:TEMP\GoogleCloudSDKInstaller.exe"
(New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", $gcloudInstaller)
& $gcloudInstaller
```

> If gcloud command is not recognized after install, use this

```$env:Path += ";$env:LOCALAPPDATA\Google\Cloud SDK\google-cloud-sdk\bin"```

# 6. MCP Toolbox

--to check

``` Test-Path "$env:USERPROFILE\.local\bin\toolbox.exe" ```

--to install

```
$ToolboxVersion = "0.27.0"
$ToolboxDir = "$env:USERPROFILE\.local\bin"
$ToolboxUrl = "https://storage.googleapis.com/genai-toolbox/v${ToolboxVersion}/windows/amd64/toolbox.exe"

New-Item -ItemType Directory -Force -Path $ToolboxDir
Invoke-WebRequest -Uri $ToolboxUrl -OutFile "$ToolboxDir\toolbox.exe"
$env:Path += ";$ToolboxDir"
```
