import subprocess
import logging
import os
import re

# Configure logging
logging.basicConfig(
    filename='dotnet_versions.log', 
    level=logging.INFO, 
    format='%(asctime)s - %(levelname)s: %(message)s'
)
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
logging.getLogger().addHandler(console_handler)

def get_dotnet_core_versions():
    try:
        # Command to get .NET Core SDK versions
        result = subprocess.run(['dotnet', '--list-sdks'], capture_output=True, text=True)
        if result.returncode == 0:
            sdk_versions = result.stdout.strip().split('\n')
            logging.info("Installed .NET Core SDKs:")
            for version in sdk_versions:
                logging.info(version)
        else:
            logging.error("Failed to get .NET Core SDKs: %s", result.stderr)

        # Command to get .NET Core Runtime versions
        result = subprocess.run(['dotnet', '--list-runtimes'], capture_output=True, text=True)
        if result.returncode == 0:
            runtime_versions = result.stdout.strip().split('\n')
            logging.info("\nInstalled .NET Core Runtimes:")
            for version in runtime_versions:
                logging.info(version)
        else:
            logging.error("Failed to get .NET Core Runtimes: %s", result.stderr)
    except Exception as e:
        logging.error("An error occurred: %s", str(e))

def get_dotnet_framework_versions():
    framework_dirs = [
        r"C:\Windows\Microsoft.NET\Framework",
        r"C:\Windows\Microsoft.NET\Framework64"
    ]

    versions = []

    for base_dir in framework_dirs:
        if os.path.exists(base_dir):
            for name in os.listdir(base_dir):
                if re.match(r"^v\d", name):
                    versions.append(name)
    
    if versions:
        logging.info("Installed .NET Framework Versions:")
        for version in versions:
            logging.info(version)
    else:
        logging.info("No .NET Framework versions found.")

try:
    get_dotnet_core_versions()
    get_dotnet_framework_versions()
except Exception as e:
    logging.error("An error occurred: %s", str(e))
finally:
    logging.info("Script execution completed.")
