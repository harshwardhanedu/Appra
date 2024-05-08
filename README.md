import subprocess

# Define the PowerShell command
powershell_command = "Get-ChildItem 'Registry::HKLM\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP' | ForEach-Object { $_.Name -replace 'HKEY_LOCAL_MACHINE\\\\SOFTWARE\\\\Microsoft\\\\NET Framework Setup\\\\NDP\\\\', '' }"

try:
    result = subprocess.run(['powershell.exe', '-Command', powershell_command], capture_output=True, text=True)
    if result.returncode == 0:
        # Successfully executed the command
        output = result.stdout.strip()
        if output:
            print("Installed .NET Versions:")
            print(output)
        else:
            print("No .NET versions found.")
    else:
        print("Error: Failed to execute the PowerShell command.")
except Exception as e:
    print(f"Error: {e}")
