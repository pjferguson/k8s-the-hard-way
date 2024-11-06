# Compute Resource Provisioning
Before starting the tutorial, I set up the following environment:

- Created a Vagrantfile which included 4 VMs running: "aphorise/debian12-arm64"
- Configured static IP addresses and network connectivity in the Vagrantfile as well. 

### Verification
- To verify ssh capabilties I ran:

    ```bash
    vagrant ssh $hostname
    ```
- After ensuring ssh was configured I made simple ping requests between hosts:  
    
    ```bash
    ping $ipaddr
    ```

### Lab 1 
- In this lab I generated and distributed ssh keys from the jumpbox. 
- I created a machines.txt file that serves as an inventory for all machines in the cluster. 
- Using a bash while loop I was able to read through the machines.txt file and copy the SSH public key to machine. 
    
    ```bash 
    while read IP FQDN HOST SUBNET; do  ssh-copy-id root@${IP} done < machines.txt
    ```
- In this section I also assigned hostnames to machines, and configured DNS entries in ```bash /etc/hosts
``` with these updated hostnames. 

### Troubleshooting
- My "server" machine would quit the sshd service with an exit code of 255. Which after doing research I now know means that ssh has failed after being executed by another process. This happened right after configuring ssh on the server.
- I decided to run commands that provided me with zero substance:
    ```bash
    systemctl restart sshd && journalctl -u sshd
    ```
- Resolution: Destroyed the "server" vagrant box and redeployed. Configured ssh and ensured that it was running properly using: 
    ```bash
    systemctl status sshd
    ```



### Summary
- Great introduction to Kubernetes terminology and architecture.



