import subprocess
import logging

# Configure logging
logging.basicConfig(filename='dotnet_versions.log', level=logging.INFO, format='%(asctime)s - %(levelname)s: %(message)s')
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
logging.getLogger().addHandler(console_handler)

# Define the PowerShell command
powershell_command = "Get-ChildItem 'Registry::HKLM\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP' | ForEach-Object { $_.Name -replace 'HKEY_LOCAL_MACHINE\\\\SOFTWARE\\\\Microsoft\\\\NET Framework Setup\\\\NDP\\\\', '' }"

try:
    result = subprocess.run(['powershell.exe', '-Command', powershell_command], capture_output=True, text=True)
    output = result.stdout.strip()
    logging.info("Installed .NET Versions:" if output else "No .NET versions found.")
except Exception as e:
    logging.error(f"Error: {e}")
finally:
    logging.info(output) if output else None
    logging.info("Script execution completed.")
