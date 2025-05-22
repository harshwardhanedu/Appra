import subprocess
import logging

logging.basicConfig(level=logging.INFO)

def get_chrome_version():
    version = None
    try:
        result = subprocess.run(['google-chrome', '--version'], capture_output=True, text=True)
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
