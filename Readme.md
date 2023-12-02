Add the below in UserData in ec2 instance 

#!/bin/bash
yum install git -y
yum install python3-devel -y
yum install gcc -y
cd /opt && git clone https://github.com/sabincloco/flaskapp.git
python3 -m ensurepip
cd /opt/flaskapp/ && pip3 install -r requirements.txt
cd /opt/flaskapp/ && echo 'uwsgi --socket 0.0.0.0:5000 --protocol=http -w wsgi:app' > start.sh
chmod +x /opt/flaskapp/start.sh
/opt/falskapp/start.sh
