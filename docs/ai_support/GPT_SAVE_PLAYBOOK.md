# GPT_SAVE_PLAYBOOK.md
**Print-only** PowerShell 5.1 template for SAVE STARFALL. Do not auto-execute in this environment.
```powershell
param([string]$SessionTag=(Get-Date -Format 'yyyyMMddHHmmss'),[string]$Passphrase=$null)
$root = Resolve-Path .
$artifactDir = Join-Path $root 'artifacts\game'
$saveZip = Join-Path $root 'Starfall_Save.zip'
$backup = "$saveZip.session_$SessionTag.bak"
if (Test-Path $saveZip) { Copy-Item $saveZip $backup -Force }
Add-Type -AssemblyName System.IO.Compression.FileSystem
[System.IO.Compression.ZipFile]::CreateFromDirectory((Resolve-Path '.'), $saveZip)
if ($Passphrase -and (Test-Path 'tools\Encrypt-SFX.ps1')) {
  & 'powershell.exe' -ExecutionPolicy Bypass -File 'tools\Encrypt-SFX.ps1' -ZipPath $saveZip -Passphrase $Passphrase
}
Copy-Item $saveZip -Destination $artifactDir -Force
if (Test-Path 'Starfall_Save.sfx.json') { Copy-Item 'Starfall_Save.sfx.json' -Destination $artifactDir -Force }
git add artifacts/game/Starfall_Save.zip _campaigns
git commit -m "[auto] Save Starfall session $SessionTag"
```
