import os
import re

def get_tomcat_version(tomcat_path):
    try:
        # Construct the path to the 'version.sh' file for Unix-like systems
        version_script_unix = os.path.join(tomcat_path, 'bin', 'version.sh')
        
        # Construct the path to the 'version.bat' file for Windows systems
        version_script_windows = os.path.join(tomcat_path, 'bin', 'version.bat')
        
        # Check if Tomcat version script exists for Unix-like systems
        if os.path.isfile(version_script_unix):
            version_script = version_script_unix
        # Check if Tomcat version script exists for Windows systems
        elif os.path.isfile(version_script_windows):
            version_script = version_script_windows
        else:
            print("Tomcat version script not found.")
            return None
        
        # Execute the version script and capture output
        result = os.popen(version_script).read()
        
        # Extract the version from the output using regex
        version_match = re.search(r'Version\s*:\s*(\d+\.\d+\.\d+)', result)
        if version_match:
            return version_match.group(1)
        else:
            print("Failed to extract Tomcat version.")
            return None
    except Exception as e:
        print("Error:", e)
        return None

# Provide the path to the Tomcat installation directory
tomcat_path = "C:/path/to/tomcat"

# Get Tomcat version
tomcat_version = get_tomcat_version(tomcat_path)
if tomcat_version:
    print("Tomcat Version:", tomcat_version)
else:
    print("Failed to fetch Tomcat version.")
