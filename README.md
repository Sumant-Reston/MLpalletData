# MLpalletData
MLpalletData is a Raspberry Pi-based machine learning system designed to count pallets and estimate their sizes using a Pi Camera.

🔧 Setup Instructions

1) Download Required Files
Place the template folder and app.py file on the Desktop of your Raspberry Pi.

2) Enable Auto-Start on Boot
Configure your Raspberry Pi to run app.py automatically on boot using systemd or another startup method.

3) Access the Web Interface
Connect your phone or device to the same network as the Raspberry Pi.
Open a browser and go to the Pi’s IP address:
http://<raspberry-pi-ip>:5000

-------------------------------------------------------------------------
****** To setup program to run from boot ********

🔧 Step 1: Create the service file

sudo nano /etc/systemd/system/camera-web.service

📝 Step 2: Paste this into the file

[Unit]
Description=Raspberry Pi Camera Flask App
After=network.target

[Service]
ExecStart=/usr/bin/python3 /home/pi/Desktop/app.py
WorkingDirectory=/home/pi/Desktop
StandardOutput=inherit
StandardError=inherit
Restart=always
User=pi

[Install]
WantedBy=multi-user.target

    ⚠️ Make sure /home/pi/Desktop/app.py exists and is correct.

💾 Step 3: Save and exit

    Press CTRL + O, then Enter to save

    Press CTRL + X to exit nano

🔁 Step 4: Reload systemd to register the service

sudo systemctl daemon-reload

🚀 Step 5: Enable it to run at boot

sudo systemctl enable camera-web.service
--------------------------------------------------------------
***** To Remove from boot *****

sudo systemctl stop camera-web.service
sudo systemctl disable camera-web.service
sudo rm /etc/systemd/system/camera-web.service
sudo systemctl daemon-reload
-------------------------------------------------------------
