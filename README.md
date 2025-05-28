import subprocess
import logging

logging.basicConfig(level=logging.INFO)

def get_chrome_version():
    version = None
    try:
        # PowerShell command to get file version of chrome.exe
        powershell_command = r'''
        (Get-Item "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe").VersionInfo.ProductVersion
        '''
        result = subprocess.run(["powershell", "-Command", powershell_command], capture_output=True, text=True)

        if result.returncode == 0:
            version = result.stdout.strip()
        else:
            logging.warning("Trying alternate path...")

            # Try 64-bit installation path
            powershell_command_alt = r'''
            (Get-Item "C:\Program Files\Google\Chrome\Application\chrome.exe").VersionInfo.ProductVersion
            '''
            result = subprocess.run(["powershell", "-Command", powershell_command_alt], capture_output=True, text=True)
            if result.returncode == 0:
                version = result.stdout.strip()
            else:
                logging.error("PowerShell failed with return code: %s", result.returncode)

    except Exception as e:
        logging.error("Error occurred while fetching Chrome version: %s", e)

    finally:
        if version:
            logging.info(f"Chrome version: {version}")
        else:
            logging.warning("Failed to fetch Chrome version.")
        logging.info("Script execution completed.")
        return version

chrome_version = get_chrome_version()
print("Detected Chrome Version:", chrome_version)
