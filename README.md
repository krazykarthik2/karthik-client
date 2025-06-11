# When you use sudo nano , it will open text editor to save after pasting text, use 
# Ctrl + O

# Project Execution Documentation

This document provides step-by-step instructions to set up and execute the `karthik-client` project, including creating a virtual environment, installing dependencies, preparing a startup script, and configuring a systemd service for automatic execution at boot.

---

## 1. Clone the Repository

Clone the project from GitHub:
```
git clone https://www.github.com/krazykarthik2/karthik-client
```

---

## 2. Set Up the Python Virtual Environment

Navigate to the project directory and create a virtual environment:
```

cd karthik-client
py -m venv venv
```


Activate the virtual environment:
```
source /home/karthik-client/venv/bin/activate
```


---

## 3. Install Project Dependencies

Install the required Python packages:
```
pip install -r requirements.txt
```


---

## 4. Create the Startup Script

Create a shell script to activate the environment and run the main script:
```

sudo nano start_direct.sh
```

Paste the following content into `start_direct.sh`:
```
#!/bin/bash
source /home/karthik-client/venv/bin/activate
python3 /home/karthik-client/direct_windowless.py
```
Make the script executable:

```
chmod +x /home/karthik-client/start_direct.sh
```

---

## 5. Create a Systemd Service

Create a new service file to run the script at boot:
```
sudo nano /etc/systemd/system/startup.service
```


Add the following content:
```
[Unit]
Description=runs the script at boot time
After=network.target

[Service]
ExecStart=/home/karthik-client/start_direct.sh
WorkingDirectory=/home/karthik-client/
Restart=on-failure
User=root

[Install]
WantedBy=multi-user.target
```

---

## 6. Enable and Start the Service

Reload systemd to recognize the new service:
```
sudo systemctl daemon-reload
```


Enable the service to start on boot:
```
sudo systemctl enable startup.service
```


Start the service immediately:
```
sudo systemctl start startup.service
```


Check the status of the service:
```
sudo systemctl status startup.service
```


---

## 7. Additional Notes

- Replace `/home/karthik-client/` with the actual path if different.
- Ensure Python 3 and `venv` are installed on your system.

---

**End of Documentation**
