Appraisal Comment:

In 2023, I focused on enhancing my digital skills, domain knowledge, and interpersonal abilities. I am currently pursuing the AZ-900 certification and have completed all mandatory trainings, including Generative AI, Value of Data Analysis, and Cloud Foundations, on time. I improved execution in Agile and Scrum methodologies and actively participated in cross-team collaboration initiatives. My contributions reflect a commitment to continuous learning, timely delivery, and driving team efficiency

.import psutil
import subprocess
import os

def get_chrome_version():
    for proc in psutil.process_iter(['name', 'exe']):
        try:
            if proc.info['name'] and 'chrome' in proc.info['name'].lower():
                chrome_path = proc.info['exe']
                if chrome_path and os.path.exists(chrome_path):
                    # Run the Chrome executable with --version to get version info
                    version_output = subprocess.check_output([chrome_path, '--version'], stderr=subprocess.STDOUT)
                    return version_output.decode().strip()
        except (psutil.AccessDenied, psutil.NoSuchProcess, psutil.ZombieProcess, FileNotFoundError):
            continue
    return "Chrome process not found or version not retrievable."

print(get_chrome_version())
