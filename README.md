import subprocess

# Define the PowerShell command
powershell_command = "Get-Service Tomcat* | Select-Object -ExpandProperty DisplayName"

# Execute the PowerShell command
try:
    result = subprocess.run(['powershell.exe', '-Command', powershell_command], capture_output=True, text=True)
    if result.returncode == 0:
        # Successfully executed the command
        output = result.stdout.strip()
        print("Output:", output)
    else:
        print("Error: Failed to execute the PowerShell command.")
except Exception as e:
    print(f"Error: {e}")
