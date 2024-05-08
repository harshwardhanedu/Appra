import subprocess
import os

def find_appcmd():
    # Search for appcmd.exe in the system PATH
    for path in os.environ["PATH"].split(os.pathsep):
        appcmd_path = os.path.join(path, "appcmd.exe")
        if os.path.isfile(appcmd_path):
            return appcmd_path
    return None

def get_iis_version_details():
    try:
        # Find the path to appcmd.exe
        appcmd_path = find_appcmd()
        if not appcmd_path:
            print("appcmd.exe not found in system PATH.")
            return None
        
        # Run the command to get IIS version details
        result = subprocess.run([appcmd_path, 'list', 'site', '/text'], capture_output=True, text=True)
        
        # Check if the command execution was successful
        if result.returncode != 0:
            print("Error executing appcmd command:")
            print(result.stderr)
            return None
        
        # Extract the version details from the output
        iis_version_details = {}
        lines = result.stdout.strip().split('\n')
        for line in lines:
            if 'IIS Version' in line:
                iis_version_details['Version'] = line.split(':')[1].strip()
            elif 'Server Comment' in line:
                iis_version_details['Server Comment'] = line.split(':')[1].strip()
        
        return iis_version_details
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
iis_version_details = get_iis_version_details()
if iis_version_details:
    print("IIS version details:")
    for key, value in iis_version_details.items():
        print(f"{key}: {value}")
else:
    print("Failed to fetch IIS version details.")
