# There will 5 vms
    # lab-start-ansible ( lab setup )

    Name                ROLE                    OS            USERNAME ( sudo )           PASSWORD

    worksation        Ansible-contorller      CentOS8       kiosk                       cmdb@123  
    node1	          Managed Host            CentOS8       devops                      cmdb@123
    node2             Managed Host            CentOS8       devops                      cmdb@123
    node3             Managed Host            Ubuntu        devops                      cmdb@123
    node4             Managed Hosts           Ubuntu        devops                      cmdb@123



# ssh  as kiosk  in worktation 


Before you begin.
      
     1.   Log in as the ubuntu user on your cloud-node and run lab-start-ansible. This setup script ensures that the 
          control node and  managed host,workstation ( control-node ) node1/2/3/4(managed hosts ), is reachable on the network.

     2.   Log in as the kiosk  user on workstation 
     
     3.   Verify that Python 3 is installed on workstation. ( if is is not installed please install python3 )
            # [kioskt@workstation ~]$ yum list installed python3
            # [kioskt@workstation ~]$ yum install  python3
     
     4.   Install Ansible on workstation so that it can be used as a control node
           # [kioskt@workstation ~]$ yum install epel-release 
           # [kioskt@workstation ~]$ yum install ansible 



     5.   Prepare to test the Ansible installation. Create a new directory, /home/kiosk/dep-install. 
          In that directory, create an Ansible inventory file named inventory.
          Follow the instructions below to edit that file so that it lists the managed host
          node1 and node2 ( user ip address of managed hosts ) as a member of the host group rpmfamily.
          node3 and node4 ( user ip address of managed hosts ) as a member of the host group debfamily.
          (The exercise will show you how to do this for now, but the course will cover how static inventory 
          files work in the next chapter.)
          
          5.1 Create and change directory to the /home/kiosk/dep-install directory.
          
            [kiosk@workstation ~]$ mkdir /home/kiosk/dep-install
            [kiosk@workstation ~]$ cd /home/kiosk/dep-instal
            
          5.2 Use a text editor to create /home/kiosk/dep-install/inventory, containing the following lines: ( replace ip with your env )
              
              [rpmfamily]
              10.0.0.1
              10.0.0.2
               
              [debfamily]
              10.0.0.3
              10.0.0.4
           

