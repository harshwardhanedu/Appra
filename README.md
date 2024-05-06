import subprocess

def get_tomcat_version():
    try:
        # Run the command to get Tomcat version
        result = subprocess.run(['%CATALINA_HOME%\\bin\\version.bat'], capture_output=True, text=True)
        
        # Check if the command execution was successful
        if result.returncode != 0:
            print("Error executing version.bat command:")
            print(result.stderr)
            return None
        
        # Extract the version from the output
        tomcat_version = None
        lines = result.stdout.strip().split('\n')
        for line in lines:
            if 'Server version' in line:
                tomcat_version = line.split(':')[1].strip()
                break
        
        return tomcat_version
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
tomcat_version = get_tomcat_version()
if tomcat_version:
    print("Installed Tomcat version:", tomcat_version)
else:
    print("Failed to fetch Tomcat version.")
