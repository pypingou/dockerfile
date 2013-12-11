# Simple docker playbook to get a fedocal instance running
#
# Version 0.1
# Written against docker-io-0.7.0-14.fc19.x86_64


## Steps required to run this playbook
# docker pull mattdm/fedora
# sudo docker build -t fedocal .
# sudo docker run -p 127.0.01:5001:5000 -i -t fedocal /bin/bash
## Once inside simply run
# ./start_fedocal

## You should be able to access fedocal at http://127.0.01:5001


from mattdm/fedora

# Update everything
run yum update -y

# Install fedocal and all its dependencies
run yum install -y fedocal git sqlite

run git clone https://github.com/fedora-infra/fedocal.git
# Set the configuration files
run cd fedocal && cp fedocal.cfg.sample fedocal.cfg
run cd fedocal && sed -i -e 's|/etc/fedocal/alembic.ini|alembic.ini|' fedocal.cfg
run cd fedocal && cp alembic.ini.sample alembic.ini
run cd fedocal && sed -i -e 's|driver://user:pass@localhost/dbname|sqlite:////var/tmp/fedocal_dev.sqlite|' alembic.ini

run yum install -y python-markdown python-docutils

run echo "cd fedocal && ./runserver" > start_fedocal

run chmod +x start_fedocal

# Create the DB
run cd fedocal && python createdb.py

#ENTRYPOINT ["cd fedocal && ./runserver"]
#ENTRYPOINT ["start_fedocal"]
EXPOSE 5000


