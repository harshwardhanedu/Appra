import subprocess
import logging

# Configure logging
logging.basicConfig(filename='firefox_versions.log', level=logging.INFO, format='%(asctime)s - %(levelname)s: %(message)s')
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
logging.getLogger().addHandler(console_handler)

def get_firefox_version():
    try:
        result = subprocess.run(['firefox', '--version'], capture_output=True, text=True)
        version = result.stdout.strip().split()[-1]
        return version
    except Exception as e:
        logging.error("Error occurred while fetching Firefox version: %s", e)
        return None
    finally:
        logging.info("Script execution completed.")

# Test the function
firefox_version = get_firefox_version()

# Logging
if firefox_version:
    logging.info("Firefox version: " + firefox_version)
else:
    logging.warning("Failed to fetch Firefox version")
