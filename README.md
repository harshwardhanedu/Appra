import subprocess

def get_dotnet_version():
    try:
        # Run the command to get installed .NET Framework versions
        result = subprocess.run(['dotnet', '--list-sdks'], capture_output=True, text=True)
        
        # Extract the versions from the output
        versions = []
        lines = result.stdout.strip().split('\n')
        for line in lines:
            if line.startswith('['):
                version = line.split('[')[1].split(']')[0]
                versions.append(version)
        
        return versions
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
dotnet_versions = get_dotnet_version()
if dotnet_versions:
    print("Installed .NET SDK versions:", dotnet_versions)
else:
    print("Failed to fetch .NET SDK versions.")
