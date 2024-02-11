# Procedure to host Fast API on AWS.

## Step 1

login to your AWS account and go to Console.
![Alt Text](Images/WhatsApp%20Image%202024-02-11%20at%2017.38.45_4301b581.jpg)

## Step 2

Go to ec2 dashboabrd and click on launch instance.
![Alt Text](Images/EC2.jpg)

## Step 3

### Step 3.1

Create an instance
![Alt Text](Images/Instance.jpg)

### Step 3.2

Choose an application and Os images
![Alt Text](Images/OS.jpg)

### Step 3.3

Choose an instance type
![Alt Text](Images/Instance_type.jpg)

### Step 3.4

Create a Key pair
![Alt Text](Images/Key_pair.jpg)
Key appears in the form of .pem file. Download it and keep it safe. It will be used to connect to the instance.

## Step 4

Network Setting
![Alt Text](Images/NS.jpg)

Launch the instance.

Click on the instance ID to see the details of the instance.
![Alt Text](Images/ID.jpg)

## Step 5

Connect to the instance.
![Alt Text](Images/Connect.jpg)

### Step 5.1

To connect to the instance via SSH client
![Alt Text](Images/SSH.jpg)

### Step 5.2

Go to the directory where the .pem file is stored and run the following command to change the mod 400

```bash
chmod 400 file_name.pem
```

### Step 5.3

Copy the SSH command and run it in the terminal.
![Alt Text](Images/SSH_command.jpg)

### Step 5.4

After succesful connection, Update the system.

Download depenedencies and install them.

```bash
Sudo apt install -y python3-pip nginx
```

Note: Nginx is used to host the Fast API on the server. It is a web server that can be used to host the Fast API. Load balancer can also be used to host the Fast API.

### Step 5.5

Create a Nginx configuration file.

```bash
sudo vim /etc/nginx/sites-enabled/fastapi_ngnix
```

### Step 5.6

Create a server block in the configuration file.

```bash
server {
    listen 80;
    server_name _(public ipv4 of the instance)_;
    location / {
        proxy_pass http://127.0.0.1:8000;
```

![Alt Text](Images/Server_block.jpg)

### Step 5.7

Restart the Nginx server.

```bash
sudo service nginx restart
```

### Step 5.8

Git clone your Repository to the instance machine.
![Alt Text](Images/Clone.jpg)

### Step 5.9

Set up your project. install all dependencies and run the python server with the following command.

```bash
python3 -m uvicorn file_name:app --host
```

# References
https://education.github.com/