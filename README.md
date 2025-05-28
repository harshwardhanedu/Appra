import subprocess
import logging
import os
import shutil

logging.basicConfig(level=logging.INFO)

def get_chrome_version():
    version = None
    try:
        # Common Chrome installation paths on Windows
        chrome_paths = [
            os.path.expandvars(r"%ProgramFiles%\Google\Chrome\Application\chrome.exe"),
            os.path.expandvars(r"%ProgramFiles(x86)%\Google\Chrome\Application\chrome.exe"),
            shutil.which("chrome")  # If in PATH
        ]

        chrome_executable = next((path for path in chrome_paths if path and os.path.exists(path)), None)

        if not chrome_executable:
            logging.error("Google Chrome executable not found on this system.")
            return None

        result = subprocess.run([chrome_executable, '--version'], capture_output=True, text=True)
        if result.returncode == 0:
            version = result.stdout.strip().split()[-1]
        else:
            logging.error("Non-zero return code: %s", result.returncode)

    except Exception as e:
        logging.error("Error occurred while fetching Chrome version: %s", e)
    finally:
        if version:
            logging.info(f"Chrome version: {version}")
        else:
            logging.warning("Failed to fetch Chrome version")
        logging.info("Script execution completed.")
        return version

chrome_version = get_chrome_version()
print("Detected Chrome Version:", chrome_version)
