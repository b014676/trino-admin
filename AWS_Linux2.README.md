# For dev setup in AWS linux2

            $ sudo yum install gcc python2-pip.noarch

## Building

1 Clone your fork locally from https://github.com/b014676/trino-admin

        $ git clone git@github.com:your_name_here/presto-admin.git

3. Install your local copy into a virtualenv. Assuming you have virtualenvwrapper installed, this is how you set up your fork for local development ::

        $ cd prestoadmin/
        $ python setup.py develop



5. When you're done making changes, check that your changes pass `make clean lint test`, which runs flake8 and the unit tests (which test both Python 2.6 and 2.7)


### Building the installer
 
        $ make dist-offline

        # Add current user to Docker group to run without sudo
        $ sudo gpasswd -a ${USER} docker
        $ sudo service docker restart
   
#### Install presto admin 

        $ tar xvf prestoadmin-<version>-offline.tar.gz
        $ cd prestoadmin
        $ ./install-prestoadmin.sh   ( the last action of install prestoadmin-2.12-py2-none-any might fail, is so process to next step.)
        $ pip install prestoadmin-2.12-py2-none-any.whl
        
##### Config presto-admin

1. run prestoadmin

        $ presto-admin
        
   This will create a .prestoadmin in user home directory
   
2.  create a config.json file in .prestoadmin directory
       
		{
		  "username": "hadoop",
		  "port": "22",
		  "coordinator": "172.31.16.188",
		  "workers": ["172.31.21.69"],
		  "java_home": "/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64"
		}
		
3. run presto-admin

        $presto-admin -i dev.pem  server status 
        
  where dev.pem is the ssh key to the emr cluster
        
