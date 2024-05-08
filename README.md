import subprocess

def get_tomcat_version():
    try:
        # Execute command to get Tomcat version
        result = subprocess.run(['version.bat'], capture_output=True, text=True, shell=True)
        # Parse the output to get the version
        version_line = next(line for line in result.stdout.splitlines() if 'Server version' in line)
        version = version_line.split(': ')[1]
        return version.strip()
    except Exception as e:
        print(f"Error: {e}")
        return None

# Get and print Tomcat version
tomcat_version = get_tomcat_version()
if tomcat_version:
    print(f"Tomcat version: {tomcat_version}")
else:
    print("Failed to retrieve Tomcat version.")
