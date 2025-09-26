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

