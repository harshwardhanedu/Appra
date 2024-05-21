import os
import re
import logging

# Configure logging
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s: %(message)s')
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
logging.getLogger().addHandler(console_handler)

def get_firefox_version():
    firefox_path = None
    try:
        program_files_dirs = [os.environ.get("ProgramFiles(x86)"), os.environ.get("ProgramFiles")]
        for program_files_dir in program_files_dirs:
            if program_files_dir:
                firefox_path = os.path.join(program_files_dir, "Mozilla Firefox", "firefox.exe")
                if os.path.isfile(firefox_path):
                    break

        if firefox_path:
            cmd = "wmic datafile where name='" + firefox_path.replace("\\", "\\\\") + "' get Version"
            result = os.popen(cmd).read()
            version_match = re.search(r"Version=(\d+\.\d+\.\d+\.\d+)", result)
            if version_match:
                return version_match.group(1)
            else:
                return None
        else:
            return None
    except Exception as e:
        logging.error("Error: %s", e)
        return None
    finally:
        logging.info("Script execution completed.")

firefox_version = get_firefox_version()

if firefox_version:
    logging.info("Firefox Version: %s", firefox_version)
else:
    logging.warning("Failed to fetch Firefox version.")
