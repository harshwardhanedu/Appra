import subprocess

def get_iis_version():
    try:
        # Run the command to get IIS version
        result = subprocess.run(['powershell', 'Get-WmiObject', '-Class', 'Win32_Service', '|', 'Where-Object', '{ $_.Name -eq "W3SVC" }', '|', 'Select-Object', '-ExpandProperty', 'DisplayName'], capture_output=True, text=True)
        
        # Check if the command execution was successful
        if result.returncode != 0:
            print("Error executing PowerShell command:")
            print(result.stderr)
            return None
        
        # Extract the version from the output
        iis_version = result.stdout.strip()
        return iis_version
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
iis_version = get_iis_version()
if iis_version:
    print("Installed IIS version:", iis_version)
else:
    print("Failed to fetch IIS version.")
