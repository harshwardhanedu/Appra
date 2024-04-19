import subprocess

def get_tomcat_version():
    try:
        output = subprocess.check_output(["catalina.bat", "version"], stderr=subprocess.STDOUT, shell=True, universal_newlines=True)
        version_start_index = output.find("Server version:")
        version_end_index = output.find("\n", version_start_index)
        version_string = output[version_start_index:version_end_index].split(": ")[1]
        return version_string.strip()
    except subprocess.CalledProcessError:
        return "Error: Apache Tomcat not found or version information not available."

# Example usage:
tomcat_version = get_tomcat_version()
print(f"The version of Apache Tomcat is: {tomcat_version}")
