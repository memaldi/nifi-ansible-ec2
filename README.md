1. Set AWS credentials at ~/.aws/credentials
2. Download SSH private key at ~/.ssh/vockey.pem
3. Set the proper permissions for the key: `chmod og-rwx ~/.ssh/vockey.pem`
4. Install requirements: `pip install -r requirements.txt`
5. Install vim and less: `sudo apt update && apt install -y vim less`
6. Edit `inventory.yml` file and replace `nifi` host DNS with hadoop_master node's **public** DNS.
8. Edit `install-nifi.yml` ("Replace nifi.web.https.host by hadoop_master host" step) and set hadoop_master node's **public** DNS.
9. Install nifi: `ansible-playbook -i inventory.yml --key-file=~/.ssh/vockey.pem --user ec2-user install-nifi.yml`
10. Create an http tunnel to access to Nifi (replace by master's public DNS):
```
ssh -i ~/.ssh/vockey.pem -N -L 8443:ec2-3-87-82-66.compute-1.amazonaws.com:8443 ec2-user@ec2-3-87-82-66.compute-1.amazonaws.com
```
11. Access nifi at https://ec2-3-87-82-66.compute-1.amazonaws.com:8443 (replace by master's public DNS).