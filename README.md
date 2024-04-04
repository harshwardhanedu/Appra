import os
import re

def get_edge_version():
    try:
        # Define the path to the msedge.exe file
        edge_path = ""
        program_files_dirs = [os.environ.get("ProgramFiles(x86)"), os.environ.get("ProgramFiles")]
        for program_files_dir in program_files_dirs:
            if program_files_dir:
                edge_path = os.path.join(program_files_dir, "Microsoft", "Edge", "Application", "msedge.exe")
                if os.path.isfile(edge_path):
                    break

        # Read the version from the file properties
        if edge_path:
            cmd = 'wmic datafile where name="' + edge_path.replace("\\", "\\\\") + '" get Version /value'
            result = os.popen(cmd).read()
            version_match = re.search(r'Version=(\d+\.\d+\.\d+\.\d+)', result)
            if version_match:
                return version_match.group(1)
        return None
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
edge_version = get_edge_version()
if edge_version:
    print("Edge Version:", edge_version)
else:
    print("Failed to fetch Edge version.")




-----------------
import os
import re

def get_firefox_version():
    try:
        # Define the path to the firefox.exe file
        firefox_path = ""
        program_files_dirs = [os.environ.get("ProgramFiles(x86)"), os.environ.get("ProgramFiles")]
        for program_files_dir in program_files_dirs:
            if program_files_dir:
                firefox_path = os.path.join(program_files_dir, "Mozilla Firefox", "firefox.exe")
                if os.path.isfile(firefox_path):
                    break

        # Read the version from the file properties
        if firefox_path:
            cmd = 'wmic datafile where name="' + firefox_path.replace("\\", "\\\\") + '" get Version /value'
            result = os.popen(cmd).read()
            version_match = re.search(r'Version=(\d+\.\d+\.\d+\.\d+)', result)
            if version_match:
                return version_match.group(1)
        return None
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
firefox_version = get_firefox_version()
if firefox_version:
    print("Firefox Version:", firefox_version)
else:
    print("Failed to fetch Firefox version.")
