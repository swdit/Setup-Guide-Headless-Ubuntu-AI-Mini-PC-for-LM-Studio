# Setup Guide: AI-Mini PC for Local-LLM hosting

## Utilities

- Mini PC with shared memory 
  
  - in this example I will use a: *Minisforum AI X1 Pro, AMD Ryzen AI 9 HX 370 / 64GB RAM*

- Ubuntu Desktop 24 LTS

- XRDP as remote desktop solution *(skip and use SSH if you want to go truely headless)*

- Fuse *(requirement for LM-Studio)*

- Assasin-AppImageLauncher *(will make LM-Studio App Installation easier)*

- LM-Studio as hosting tool for local LLM's

- Startup

# Installing Ubuntu

1. Flash a USB Stick with Ubuntu 24 LTS 
   
   1. **Important**:  Kernel Versions newer than 6.16 currently struggle with AMD iGPU support; you will likely not have the Vulcan-Graphics-Acceleration available. You'd be running your LLM on CPU only, suffering great speed losses in terms of tokens per second.

2. Enter you Mini-PC's UEFI
   
   1. Deactivate *"Secure Boot"* (can be reactivated later)
   
   2. Set USB to slot one in Boot-Order Settings

3. Plug in the USB Stick and reboot

4. Follow the setup guide
   
   1. Consider switching off *"require passwort at startup"* this will make unsupervised reboot easier with the obvious security downside.

# Installing XRDP as RemoteDesktop solution

*To avoid some issues with the RDP solutions build into Ubuntu (keyring issues on reboot with) we will go for  XRDP.*

1. `sudo apt install xrdp`

2. Check status of XRDP: ( XRDP runs automatically after installation)
   
   `sudo systemctl status xrdp`

3. add the xrdp user to the ssl-cert group
   `sudo adduser xrdp ssl-cert`

4. Restart xrdp service:
   `sudo systemctl restart xrdp`

5. get your Mini-PCs IP-Adress
   `ip addr`

6. Configuring Firewall
   Replace the IP-Adress with the one you just retrieved.
   `sudo ufw allow from 192.168.33.0/24 to any port 3389`
   `sudo ufw allow 3389`

Use a Remote Desktop Client of your choice on an different computer to access the Mini-PC via XRDP

The Login credentials alre equal to the local user account on the Mini-PC

**Important**: You must be logged out on the Mini-PC in order to connect via XRDP
**Important**: Make sure you the build in RDP tools and if applicable thrid party RDP tools are not running.



# Install Fuse

LM-Studio requires Fuse to run on Ubuntu

`sudo apt install libfuse2  `



# Install AppImageLauncher

LM-Studio is only available as .app image at the time of writing this guide.

The installation can be done without additional tools but it will be easier if you use an AppImage loader like assasin.



1. Download AppImageLauncher
   [https://github.com/TheAssassin/AppImageLauncher/releases/]()

2. Install AppImageLauncher



# Install LM-Studio

1. Download LM-Studio Linux Version 
   [https://lmstudio.ai/download]()

2. Open LM-Studio .app file using AppImageLoader

3. click *"Integrate and Run"*

4. Testrun LM-Studio

5. Check if the Vulcan iGPU appears under *LM-Studio/Settings/Hardware

6. Download LLM's of your choice
   
   1. Recommendations in Dec. 2025
      
      1. Gemma 3 12B
      
      2. Gemma 3 4B
      
      3. 
      
      4. Qwen 3 4B 2507



# Setup-Autostart

1. Open Ubuntus build in Startup tool

2. Name it as of your taste and browse for LM-Studio App located in the Apllications folder (AppLauncherDefault)

3. add this flag behind the path sepparated by one whitespace
   `--no-sandbox`
