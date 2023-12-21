Support in Audit and Compliance Activities
• Outcome: Successfully contributed to the improvement of platform teams' security and compliance posture
• Metrics: No major compliance instances reported for 2023.
• Training: Ensured all compliance trainings were completed without reminders or defaulters
• Documentation: Achieved documentation capture rate by consistently following audit and compliance processes.
Team Collaboration & Team Player.
• Demonstration: Actively collaborated with team members, embodying EXL values of Collaboration, Respect, and Integrity.
• Reporting: Provided accurate internal and external status reports.
*Adherence: Strictly adhered to organization directives and policies issued periodically.
Overall, successfully met the outlined goals, contributing to a robust audit and compliance framework while fostering a collaborative team environment and upholding organizational values.


----------

Adherence to Agile Principles:
• Successfully increased Agile adoption within projects, showcasing commitment to agile principles.
• Effectively demonstrated agility by adapting to changes and addressing challenges promptly.
Task Delivery:
• Consistently tried to deliver assigned tasks with a sprint of schedule variance, showcasing the reliability.
• Achieved the goal of delivering tasks within planned effort, demonstrating efficient time management skills.
Defect Management:
• Demonstrated a proactive approach to quality assurance by reporting and creating Jira tickets for identified bugs and defects.
Risk Management:
• Timely identification and addressing of risks/issues highlight a proactive approach to risk management.



• Ability to prioritize tasks effectively contributed to addressing critical issues promptly.
Defect Leakage in UAT:
• The goal of keeping defect leakage in UAT stage, showcasing a thorough and effective testing process.
Process Adherence and Enhancement:
• Demonstrated commitment to defined processes by adhering to them regularly.
• Proactively contributed to process improvement by establishing/enhancing templates, guidelines, checklists, and standards for the project and team.
Overall, the commitment to Agile principles, efficient task delivery, proactive defect management, and adherence to processes contribute significantly to the overall Delivery Excellence, showcasing a high level of organizational and
individual effectiveness.

--------------

Overall, consistently demonstrated commitment to quality project delivery through adherence, precision, efficient practices, and continuous improvement.

• Proactively contributed to process improvement by enhancing project templates, guidelines, checklists, and standards.

Continuous Improvement:

• Adhered to Configuration Management and Project guidelines, ensuring consistency and reliability in project processes.

Guideline Adherence:

• Actively participated in cross-functional activities, enhancing overall project understanding and efficiency.

Cross-functional Collaboration:

• Delivered high important tasks efficiently, on time, and with high quality, emphasizing proper utilization, productivity, and accountability.

Efficient Delivery:

• Kept business documents updated for application changes, ensuring clear communication and alignment with evolving requirements.

Communication and Updates:

• Accurately updated JIRA for 100% working days, showcasing meticulous time logging and status updates.
• Captured technical specs for tasks, enriching our Knowledge Repository.

Documentation Precision:

• Consistently achieved 80% adherence across all project categories, ensuring quality in each aspect.



------------


Digital Skills and Domain Knowledge:
• Proactively acquired digital skills through diverse tasks such as gem graph generation, regression analysis, and API creation.
• Demonstrated hands-on experience in raising defects and providing regression analysis, showcasing improved domain knowledge.
Agile and Scrum Execution:
• Matured execution in Agile and Scrum methodologies, evident in tasks like release checklist, Regression analysis implementation.
• Successfully contributed to research tasks, including gem graph generation using Robocop, git pre commit hook. disable edge sidebar highlighting adaptability to new tools and methodologies.
Continuous Learning:
• Actively pursuing continuous learning and exploring etoud technologies and Microsoft Azure solutions for Care Radius
Training Completion:
• Timely completed assigned trainings, displaying a commitment to professional development and staying current with industry standards.
Certifications:
• Initiated the process illustrating dedication to personal and professional growth.
Cross-Team Collaboration:
• Actively participated in cross-team collaboration by providing knowledge transfer for new teammates, creating Confluence pages, and initiating collaborative initiatives for problem-solving.
• Contributed to the team's knowledge base by writing a Git pre-commit hook and providing KT for onboarding. - fostering a collaborative learning environment.

Overall, the commitment to acquiring digital skills, enhancing domain knowledge, embracing new technologies, and fostering collaboration showcases significant self-development. The completion of trainings and contributions to research tasks further affirm dedication to staying at the forefront of industry advancements.


--------
Consistently excelled in project delivery, exceeding adherence targets and ensuring efficient, quality outcomes. Demonstrated proactive commitment to audit and compliance, enhancing security posture across teams. Actively pursued self-development, acquiring digital skills and contributing to cross-team collaboration. Successfully expanded automation testing coverage, fostering a collaborative testing environment.



import psutil
import paramiko

def get_remote_system_info(hostname, username, password):
    # Connect to the remote machine
    ssh = paramiko.SSHClient()
    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    ssh.connect(hostname, username=username, password=password)

    # CPU information
    cpu_info = {
        'CPU Cores': psutil.cpu_count(logical=False),
        'Logical CPUs': psutil.cpu_count(logical=True),
        'CPU Usage (%)': psutil.cpu_percent(interval=1),
    }

    # Memory information
    mem_info = {
        'Total Memory (GB)': round(psutil.virtual_memory().total / (1024 ** 3), 2),
        'Used Memory (GB)': round(psutil.virtual_memory().used / (1024 ** 3), 2),
        'Free Memory (GB)': round(psutil.virtual_memory().free / (1024 ** 3), 2),
    }

    # Disk information
    disk_info = {
        'Total Disk Space (GB)': round(psutil.disk_usage('/').total / (1024 ** 3), 2),
        'Used Disk Space (GB)': round(psutil.disk_usage('/').used / (1024 ** 3), 2),
        'Free Disk Space (GB)': round(psutil.disk_usage('/').free / (1024 ** 3), 2),
    }

    # Network information
    net_info = {
        'Network Interfaces': psutil.net_if_list(),
        'Network Usage': psutil.net_io_counters(pernic=True),
    }

    # Close the SSH connection
    ssh.close()

    return {
        'CPU Info': cpu_info,
        'Memory Info': mem_info,
        'Disk Info': disk_info,
        'Network Info': net_info,
    }

if __name__ == "__main__":
    # Replace these values with your remote machine details
    remote_hostname = 'your_remote_hostname'
    remote_username = 'your_remote_username'
    remote_password = 'your_remote_password'

    remote_system_info = get_remote_system_info(remote_hostname, remote_username, remote_password)
    for category, info in remote_system_info.items():
        print(f'{category}:\n{info}\n')

