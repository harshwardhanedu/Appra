import subprocess
import logging

# Set up logging
logging.basicConfig(filename='chrome_versions.log', level=logging.INFO,
                    format='%(asctime)s - %(levelname)s: %(message)s')
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
logging.getLogger().addHandler(console_handler)

def get_chrome_version():
    try:
        result = subprocess.run(
            ['wmic', 'datafile', 'where', 
             "name='C:\\\\Program Files (x86)\\\\Google\\\\Chrome\\\\Application\\\\chrome.exe'", 
             'get', 'Version', '/value'],
            capture_output=True, text=True
        )
        output = result.stdout.strip()
        version = output.split('=')[-1] if '=' in output else None

        if version:
            logging.info(f"Chrome version: {version}")
        else:
            logging.warning("Chrome not found or version not retrieved")

        return version
    except Exception as e:
        logging.error("Error fetching Chrome version: %s", e)
        return None

# Execute
chrome_version = get_chrome_version()
