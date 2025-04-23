import subprocess
import shutil
import logging
import os

logging.basicConfig(filename='chrome_versions.log', level=logging.INFO,
                    format='%(asctime)s - %(levelname)s: %(message)s')
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
logging.getLogger().addHandler(console_handler)

def get_chrome_version():
    version = None
    chrome_commands = ['chrome', 'google-chrome']  # Fallbacks
    paths_to_check = [
        shutil.which(cmd) for cmd in chrome_commands
    ] + [
        r"C:\Program Files\Google\Chrome\Application\chrome.exe",
        r"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe"
    ]

    try:
        for path in paths_to_check:
            if path and os.path.exists(path):
                result = subprocess.run([path, '--version'], capture_output=True, text=True)
                version = result.stdout.strip()
                return version

        raise FileNotFoundError("Chrome not found in known paths.")
    except Exception as e:
        logging.error("Error occurred while fetching Chrome version: %s", e)
        return None
    finally:
        if version:
            logging.info(f"Chrome version: {version}")
        else:
            logging.warning("Failed to fetch Chrome version")
            logging.info("Script execution completed.")

chrome_version = get_chrome_version()
