import subprocess
import logging

logging.basicConfig(level=logging.INFO)

def get_chrome_version():
    version = None
    try:
        # Use wmic to query the file version of chrome.exe
        result = subprocess.run(
            ['wmic', 'datafile', 'where', 'name="C:\\\\Program Files (x86)\\\\Google\\\\Chrome\\\\Application\\\\chrome.exe"', 'get', 'Version', '/value'],
            capture_output=True, text=True
        )

        if result.returncode == 0:
            output = result.stdout.strip()
            if "Version=" in output:
                version = output.split('=')[1].strip()
            else:
                logging.warning("Chrome not found at default path, trying alternate path...")

                # Try 64-bit installation path
                result = subprocess.run(
                    ['wmic', 'datafile', 'where', 'name="C:\\\\Program Files\\\\Google\\\\Chrome\\\\Application\\\\chrome.exe"', 'get', 'Version', '/value'],
                    capture_output=True, text=True
                )
                output = result.stdout.strip()
                if "Version=" in output:
                    version = output.split('=')[1].strip()

        else:
            logging.error("WMIC command failed with return code: %s", result.returncode)

    except Exception as e:
        logging.error("Exception occurred while fetching Chrome version: %s", e)

    finally:
        if version:
            logging.info(f"Chrome version: {version}")
        else:
            logging.warning("Failed to fetch Chrome version.")
        logging.info("Script execution completed.")
        return version

chrome_version = get_chrome_version()
print("Detected Chrome Version:", chrome_version)
