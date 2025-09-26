# Task-4 : Setup and Use a Firewall on Windows/Linux

### Step 1 : Check if UFW is installed
`sudo ufw version` <br>
If not installed <br>
`sudo apt update`  <br>
`sudo apt install ufw -y`

### Step 2 : Enable UFW (turn it on)
`sudo ufw enable` <br>
Check status: <br>
`sudo ufw status verbose`

### Step 3 : View current firewall rules
`sudo ufw status numbered`

### Step 4 : Block inbound traffic on Telnet (port 23)
`sudo ufw deny 23` <br>
Check new rules: <br>
`sudo ufw status numbered`
(screenshots provided)

### Step 5 : Test the Telnet block
Install telnet client (if not installed)<br>
`sudo apt install telnet -y` <br>
Try connecting to port 23 <br>
`telnet 127.0.0.1 23`
#### Expected output:Connection refused/ Unable to connect

### Step 6 : Allow SSH(port 22)
`sudo ufw allow 22` <br>
Check rules <br>
`sudo ufw status numbered`
#### We should be able to see: 
`[ 4] 22 ALLOW IN Anywhere`
#### This ensures SSH is accessible for management while Telnet remains blocked.

### Step 7 : Test SSH
`ssh local host`
#### Issue I faced here is:
`ssh: connect to host localhost port 22: Connection refused`
#### Solution to the issue i faced:
1. Check if ssh server is installed: <br>
`sudo systemctl status ssh` <br>
Upon using this command I could tell why my `ssh localhost` failed. <br>
### Because
1. By default, UFW rules allowed port 22, but my SSH daemon (sshd) has been configured to use port 3435.
2. So connections to port 22 are refused because nothing is listening there.

### Step 8 : Allow the correct SSH port in UFW
`sudo ufw allow 3435` <br>
Check rules: 
`sudo ufw status numbered`

### Step 9: Test SSH on the correct port
`ssh -p 3435 localhost`  
This allowed connection

### Step 10: Clean up rules
1. Check current firewall rules  
`sudo ufw status numbered`

2. Delete test rules
```
sudo ufw delete 8   # 3435 (v6)
sudo ufw delete 7   # 22 (v6)
sudo ufw delete 6   # 23 (v6)
sudo ufw delete 4   # 3435
sudo ufw delete 3   # 22
sudo ufw delete 2   # 23
```
### Step 11 : Disable UFW completely
```
sudo ufw disable
sudo ufe reset          ( confirm with y when prompted)
sudo ufw status verbose ( should show inactive)
```
1. `sudo ufw disable` → stopped the firewall completely and prevented it from starting on boot.
2. `sudo ufw reset` → deleted all custom rules (including lab rules and any other added rules) and restored UFW to its factory defaults.
3. `sudo ufw status verbose` → inactive confirms no firewall is running, so Ubuntu is back to a neutral state.

