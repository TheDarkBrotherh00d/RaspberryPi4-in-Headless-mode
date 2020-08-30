## Raspberry Pi 4 in Headless mode
### Requirements
Besides the Raspberry Pi, you will also need;
- MicroSD Card (8GB or more)
- A copy of RaspberryPiOS.img 
- A copy of Balena Etcher (To flash the RaspberryPiOS.img to the MicroSD Card)
- A wireless network (Router broadcasting wireless internet)

### Recommendations
- Ensure you are using a reliable MicroSD Card. This guide uses a 32GB SanDisk Ultra 10mbps card.
- If your PC does not come with a MicroSD Card slot, use a MicroSD Card adapter or USB to MicroSD.

### Step 1: Download Etcher and Raspberry Pi OS
If you have not done so already here are the links:
- [Balena Etcher](https://www.balena.io/etcher/)
- [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/)

I recommend downloading the "Raspberry Pi OS (32-bit) with desktop and recommended software" image.

### Step 2: Format and Partition the MicroSD Card
1. Once you have insered the MicroSD Card, launch Balena Etcher and select the Raspberry Pi OS as the file to flash from.
2. Select the Target device where you want Etcher to flash the image file to. Select your MicroSD Card.
3. Begin the flashing process.

### Step 3: Create 2 files in the Boot:/ Directory 
Once the flashing is complete, your computer may prompt you to Format the card. **DO NOT** format the card because it will erase the Raspberry OS.
1. **OPTIONAL** You can navigate to File Explorer Ribbon Toolbar and enable "File name extensions". This will reveal all file extension types for every file on your system.
2. Open the BOOT Partition in File Explorer and create two Text Documents. 
   - Name the first document `SSH` with no file extensions
   - Name the second document `wpa.supplicant.conf` (make sure `.conf` extension is included otherwise the raspberry pi will not read the file)

We need the `SSH` file because we will be using the SSH protocol to connect to our Pi using a Terminal. 

We also need the `wpa` file because we will be connecting the Pi to our wireless network.

### Step 4: Setting up wireless for the Pi 
1. Open the `wpa.supplicant.conf` file in Notepad and copy/paste this code in the file.
```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="NETWORK-NAME"
    psk="NETWORK-PASSWORD"
}
```
The code tells your Pi details such as the:
- The country you are in
- What the wireless programme is
- Configuring updates
- Your wireless network details such as the SSID and PASSPHRASE

**NOTE** You need to change the `ssid=` and the `psk=` to your wireless network name and password. For example, my wireless network which I will be connecting too is called `SPEED-K9`. So the `ssid=` will be `ssid=SPEED-K9` followed by the wireless password `psk=MyPa$$w0rd`.

### Step 5: Powering up and connecting to the Pi
Safely eject the card, insert it into the Pi and power it ON. 
If everything goes well, the Pi should be connected to the wireless network. You can find this out by opening a Terminal/Command Prompt and typing
`SSH raspberrypi -4`.
The default account name and password is `pi/raspberry`.
You can also find out but looking into your routers wireless devices list. If you can see the RaspberryPi listed, it has sucessfully connected.  

**NOTE** If you are unable to connect to the Pi or view it listed in your router, this is because the Pi did not connect to your wireless network. Repeat Steps 3 and 4.

