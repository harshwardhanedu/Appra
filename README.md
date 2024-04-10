import platform
import socket
import psutil

def get_machine_info():
    try:
        # Get operating system information
        os_name = platform.system()
        os_version = platform.version()

        # Get IP address
        hostname = socket.gethostname()
        ip_address = socket.gethostbyname(hostname)

        # Get RAM information
        ram = psutil.virtual_memory()
        ram_total = ram.total // (1024**3)  # Convert bytes to gigabytes

        # Get storage information
        storage = psutil.disk_usage('/')
        storage_total = storage.total // (1024**3)  # Convert bytes to gigabytes

        return {
            'OS': os_name,
            'OS Version': os_version,
            'IP Address': ip_address,
            'RAM': f"{ram_total} GB",
            'Storage': f"{storage_total} GB"
        }
    except Exception as e:
        print("Error:", e)
        return None

# Test the function
machine_info = get_machine_info()
if machine_info:
    for key, value in machine_info.items():
        print(f"{key}: {value}")
else:
    print("Failed to fetch machine information.")
