#!/bin/bash
if [ "$(basename `pwd | cut -f -4 -d '/'`)" != "home" ]; then
	echo "Please run this script in /home/ directory"
	exit 1
fi
PROJECT_NAME="mezzashop"
echo "Input project name:"
read req
if [ "$req" != "" ]; then
	PROJECT_NAME=$req
fi

echo "Install python-setuptools python-dev build-essential python-pip python-virtualenv? y/n"
read req
if [ "$req" == "y" ]; then
	apt-get install python-setuptools python-dev build-essential python-pip python-virtualenv install python-imaging
fi

if [ ! -d "Django-$PROJECT_NAME" ]; then
	mkdir "Django-$PROJECT_NAME"
fi

cd "Django-$PROJECT_NAME"
echo "Create virtualenv? y/n"
read req
if [ "$req" == "y" ]; then
	virtualenv --no-site-packages env
fi
echo "install cartridge? y/n"
read req
if [ "$req" !== "y" ]; then
	exit 1	
fi
pip install -U cartridge -E env/
. env/bin/activate

if [ ! -d "$PROJECT_NAME" ]; then
	mkdir "$PROJECT_NAME"
fi
mezzanine-project -a cartridge "$PROJECT_NAME"
cd "$PROJECT_NAME"

echo "Create DB? y/n"
cd ..
read req
if [ "$req" == "y" ]; then
	python manage.py createdb --noinput
#	python manage.py syncdb --all
#	python manage.py migrate --fake
fi

python manage.py runserver 54.194.217.161:8008
#pkill -f "python manage.py runserver"


echo "Installation copleted."

