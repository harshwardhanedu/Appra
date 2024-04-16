import os
import re

def get_tomcat_version(tomcat_path):
    try:
        # Construct the path to the server.xml file
        server_xml_path = os.path.join(tomcat_path, 'conf', 'server.xml')

        # Read the server.xml file
        with open(server_xml_path, 'r') as file:
            server_xml_content = file.read()

        # Search for the version information in the server.xml content
        version_match = re.search(r'<Server version="Apache Tomcat/(.*?)"', server_xml_content)
        if version_match:
            return version_match.group(1)
        else:
            print("Tomcat version not found in server.xml.")
            return None
    except Exception as e:
        print("Error:", e)
        return None

# Provide the path to the Tomcat installation directory
tomcat_path = "C:/path/to/tomcat"

# Get Tomcat version
tomcat_version = get_tomcat_version(tomcat_path)
if tomcat_version:
    print("Tomcat Version:", tomcat_version)
else:
    print("Failed to fetch Tomcat version.")
