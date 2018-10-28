Getting Started

Step 1: Install Python 3, using brew on Mac
Step 2: Installed Ansible
Step 3: Upon running the following command to see if Ansible is up and running I got error on Mac

ansible all -m ping

         [WARNING]: Unable to parse /etc/ansible/hosts as an inventory source
         [WARNING]: No inventory was parsed, only implicit localhost is available
         [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
         [WARNING]: Could not match supplied host pattern, ignoring: kube-master
         
Debugged Step 3, by finding that I did not have inventory source defined in the default location /etc/ansible/hosts. Updated the following to add basic updates to the inventory source

sudo mkdir /etc/ansible/
sudo touch /etc/ansible/hosts
sudo chmod 777 /etc/ansible/hosts
sudo echo "localhost ansible_connection=local" >> /etc/ansible/hosts

Thanks to for the above suggestion (https://groups.google.com/d/msg/ansible-project/W1E2gJEfRls/UE1tTsC1BgAJ)

Now I get a confirmation that Ansible is running
ansible all -m ping
  
  localhost | SUCCESS => {
      "changed": false, 
      "ping": "pong"
  }
