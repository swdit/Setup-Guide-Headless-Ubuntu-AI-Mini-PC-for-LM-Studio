# Setup Guide: AI-Mini PC for Local-LLM hosting

## Utilities

- Mini PC with shared memory 
  
  - in this example I will use a: *Minisforum AI X1 Pro, AMD Ryzen AI 9 HX 370 / 64GB RAM*

- Ubuntu Desktop 24 LTS

- XRDP as remote desktop solution (skip and use SSH if you want to go truely headless)

- LM-Studio as hosting tool for local LLM's



# Installing Ubuntu

1. Flash a USB Stick with Ubuntu 24 LTS 
   
   1. **Important**:  Kernel Versions newer than 6.16 currently struggle with AMD iGPU support; you will likely not have the Vulcan-Graphics-Acceleration available. You'd be running your LLM on CPU only, suffering great speed losses in terms of tokens per second.

2. Enter you Mini-PC's UEFI
   
   1. Deactivate "Secure Boot" (can be reactivated later)
   
   2. Set USB to slot one in Boot-Order Settings

3. Plug in the USB Stick and reboot

4. Follow the setup guide
   
   1. Consider switching off *"require passwort at startup"* this will make unsupervised reboot easier with the obvious security downside.

# Installing XRDP as RemoteDesktop solution

*To avoid some issues with the RDP solutions build into Ubuntu (keyring issues on reboot with) we will go for  XRDP.*

1. `sudo apt install xrdp`
   
   

2. Check status of XRDP: ( XRDP runs automatically after installation)
   
   1.  sudo systemctl status xrdp
   
   4. add the xrdp user to the ssl-cert group

3. 

# 
