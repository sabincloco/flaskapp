# Automated Code Deployment on EC2 Instance

This script automates the deployment process of a Flask application on an Amazon EC2 instance. The provided script includes necessary setup steps to get the application running seamlessly.

## Included Steps

1. **Git Installation:**
   - Installs Git to facilitate code retrieval from the specified repository.

2. **Python3 and Dependencies**
    - Installs Python3 development packages and GCC, crucial for Python-based application execution

3. **Repository Cloning:**
   - Clones the Flask application from the GitHub repository (`https://github.com/sabincloco/flaskapp.git`) into the `/opt` directory.

4. **Python Environment Configuration:**
    - Ensures pip is installed

5. **Installation of Application Dependencies:**
   - Installs the required Python packages specified in `requirements.txt`.

6. **Creation of Startup Script:**
   - Generates a startup script (`start.sh`) within the Flask application directory to initialize the Flask app using uWSGI on port 5000.

7. **Permission Adjustment:**
   - Grants executable permission to the `start.sh` script.

8. **Launch of Application:**
   - Executes the `start.sh` script to launch the Flask application.

## Usage Instructions

1. Ensure you have an EC2 instance running with appropriate permissions to execute these commands.
2. Copy and paste the script into the EC2 instance's User Data section while launching the instance.

### User Data Script

```bash
#!/bin/bash
yum install git -y
yum install python3-devel -y
yum install gcc -y
cd /opt && git clone https://github.com/sabincloco/flaskapp.git
python3 -m ensurepip
cd /opt/flaskapp/ && pip3 install -r requirements.txt
cd /opt/flaskapp/ && echo 'uwsgi --socket 0.0.0.0:5000 --protocol=http -w wsgi:app' > start.sh
chmod +x /opt/flaskapp/start.sh
/opt/flaskapp/start.sh
```
