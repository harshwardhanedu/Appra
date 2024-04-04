import os
import re

def get_ie_version():
    try:
        # Define the path to the iexplore.exe file
        ie_path = os.path.join(os.environ.get("ProgramFiles"), "Internet Explorer", "iexplore.exe")

        # Read the version from the file properties
        if os.path.isfile(ie_path):
            cmd = 'wmic datafile where name="' + ie_path.replace("\\", "\\\\") + '" get Version /value'
            result = os.popen(cmd).read()
            version_match = re.search(r'Version=(\d+\.\d+\.\d+\.\d+)', result)
            if version_match:
                return version_match.group(1)
        return None
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
ie_version = get_ie_version()
if ie_version:
    print("Internet Explorer Version:", ie_version)
else:
    print("Failed to fetch Internet Explorer version.")
