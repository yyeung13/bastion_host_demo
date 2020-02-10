# Bastion Host Demo

Demonstrate how to use Bastion Host to connect to Private OCI instances

You will need Bastion Host if you have large no of private OCI instances without public IP but occassionally need to SSH to them


1. Create a New Compute with Public IP

- Generate RSA key pair with command 'ssh-keygen', you can use default location and default key name 'id_rsa'. The key will be stored in <HOME>/.ssh
- Provision new Compute with the public key in id_rsa.pub
  
2. Create a New Compute with Private IP

- You can either generate a new RSA key pair with the same command above, or reuse the same
- Provision new Compute with the public key in id_rsa.pub

3. Connect Bastion Host
- In Debian, store the key pair from Bastion host in .ssh/id_rsa
- SSH to Bastion Host with 'ssh -a opc@<bastion_host_ip>', this will automatically use the default key id_rsa. If you use different key, use '-i' option to specify key location
- You should be inside Bastion Host now

4. Connect to Private Host

- Edit sshd_config by 'sudo vi /etc/ssh/sshd_config' and uncomment the line 'AllowAgentForwarding yes'
- Run ssh-agent by running 'ssh-agent'
- Put the key pair for Private Host in Bastion Host's local folder, e.g., use folder .ssh and name 'id_rsa'. If this is too confusing, use a different name
- UNIX doesn't like this file to be accessible by other users, so change the permission with 'chmod 700 id_rsa'
- Now you can SSH to private host with 'ssh opc@<private_host_ip>'

