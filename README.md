import subprocess

def get_iis_version():
    try:
        # Run the command to get IIS version
        result = subprocess.run(['%windir%\\system32\\inetsrv\\appcmd.exe', 'list', 'site', '/version'], capture_output=True, text=True)
        
        # Check if the command execution was successful
        if result.returncode != 0:
            print("Error executing appcmd command:")
            print(result.stderr)
            return None
        
        # Extract the version from the output
        iis_version = None
        lines = result.stdout.strip().split('\n')
        for line in lines:
            if 'IIS Version' in line:
                iis_version = line.split(':')[1].strip()
                break
        
        return iis_version
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
iis_version = get_iis_version()
if iis_version:
    print("Installed IIS version:", iis_version)
else:
    print("Failed to fetch IIS version.")p
