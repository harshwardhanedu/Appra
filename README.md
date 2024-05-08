import subprocess

def get_ie_version():
    try:
        # Use subprocess to execute the ver command and capture the output
        result = subprocess.run(['cmd', '/c', 'ver'], stdout=subprocess.PIPE, stderr=subprocess.PIPE, check=True, text=True)
        output = result.stdout

        # Search for Internet Explorer version in the output
        ie_version_line = [line for line in output.split('\n') if 'Internet Explorer' in line]
        if ie_version_line:
            ie_version = ie_version_line[0].split(' ')[-1].strip()
            return ie_version
        else:
            return None
    except subprocess.CalledProcessError as e:
        print("Error:", e)
        return None

ie_version = get_ie_version()
if ie_version:
    print("Internet Explorer version:", ie_version)
else:
    print("Internet Explorer not found or an error occurred.")
