import subprocess
import logging

# Configure logging
logging.basicConfig(filename='chrome_versions.log', level=logging.INFO, format='%(asctime)s - %(levelname)s: %(message)s')
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
logging.getLogger().addHandler(console_handler)

def get_chrome_version():
    try:
        result = subprocess.run(['google-chrome', '--version'], capture_output=True, text=True)
        version = result.stdout.strip().split()[-1]
        return version
    except Exception as e:
        logging.info("Error:", e)
        return None

# Test the function
chrome_version = get_chrome_version()
if chrome_version:
    logging.info("Chrome version: " + chrome_version)
else:
    logging.warning("Failed to fetch Chrome version")
