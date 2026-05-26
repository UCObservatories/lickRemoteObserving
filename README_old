# lickRemoteObserving

These scripts are to be used by remote sites to connect to Lick for remote observing.

When everything is properly configured, all you need to do is run
```
cd ~/lickRemoteObserving
./start_nickel_viewer
```
or
```
cd ~/lickRemoteObserving
./start_shane_viewer
```
to enable the connection.

You can just double click the correct script in the Finder on a Mac as well.

# Outline

- Email who will observe and request the certificate
- Install the software if you have not
- Configure the software for your computer **can reuse Keck version**
- Run Open VPN or Tunnelblick using certificate
- Open a terminal
- Test software and connection
- Go to directory with software installed
- ```./start_shane_viewers``` or ```./start_nickel_viewers```
- Type the VNC password for each VNC window

# Notify Lick of your intent to connect remotely
Before you can connect to Lick remotely, we need to provide you with the VPN info and passwords for the VNC.  As well, we need info about your remote observing station.

- Email `sa@ucolick.org` with the following info about your remote site 48 hours in advance:
    - Who will be observing
    - Phone # in case a network failure

- Email `lick-home-obs@ucolick.org` for the VPN certificate with:
   - Name of the PI
   - Date of observing nights
   - Telescope being used

Once we receive your request, we will respond with instructions on
obtaining the VPN verification. Your observing team will be emailed a
certificate(s) for that observing run.


# Familiarize Yourself with Remote Operations

We have extensive instructions for
[Nickel Remote Operations](http://mthamilton.ucolick.org/techdocs/remoteObs/nickel/intro/)
and
[Shane Remote Operations](http://mthamilton.ucolick.org/techdocs/remoteObs/shane/intro/)

# Hardware Setup

## Displays

The primary hardware requirement for running Lick VNCs is screen space.

We recommend you use the largest monitors you available. If you have
access to a large HDMI TV and the appropriate cables, that is also a
solution though it maybe less readable.

## Computer Recommendations

The following hardware configuration has been tested:

- Computer: MacBook 13" Pro (2015)
    - CPU: Intel Core i7 CPU
    - RAM: 16GB
	- an old Samsung 24" 1920x1200 that was lying around
	- Running Mojave (10.14)

- Computer: MacBook 13" Pro (2013)
  - CPU: Intel Core i5 CPU
  - RAM: 8 GB
  - Running Sierra (10.12)

- Computer: 5th generation Intel Core i5
  - 16 GB RAM
  - Linux Mint 19.3




The ability to use more than one monitor can be helpful. The Shane and
the Nickel are setup to have 6 virtual desktops, and at least 3 are
required for observing.

# Software Installation

## Outline

Here is a list of what is required

- OpenVPN or Tunnelblick
- A VNC Client
- A terminal client (xterm or iTerm or the Terminal)
- Python 3 from Anaconda3 or miniconda3

## Install Software Dependencies

NOTE: Examples below assuming sudo/root installation for all users and were originally written for linux (CentOS).  Modify as appropriate for your local OS.

The software has been tested for macOS and some Linux variants.

- Install VNC viewer client
    - **For Linux**
        - **On Linux:** TigerVNC is recommended as the VNC client.
        RealVNC has been tested as well.
		- On CentOS
        ```
        sudo yum install tigervnc-x86_64
		```
		- For Ubuntu flavors:
		```
		apt install tigervnc-viewer
		apt install tigervnc-common
    apt install tigervnc-tools
		```
        - **Important!** If you are using TigerVNC, in the $HOME/.vnc directory, create a file `default.tigervnc` with these two lines:
        ```
        TigerVNC Configuration file Version 1.0
        RemoteResize=0
        ```
        - **On Linux:** (optional) Install wmctrl (Used for auto-positioning VNC windows)
            ```
            sudo yum install epel-release
            sudo yum install wmctrl
            ```
    - **For macOS**
        - **On macOS**: Real VNC's
          [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)
          is recommended (note, this is the free software, you do not
          need VNC Viewer Plus).

        - **On macOS**: It is also possible to use the built in VNC
          viewer on macOS, but we have seen a few instances where the
          screen freezes and the client needs to be closed and
          reopened to get an up to date screen.  To select this use
          the second option in the config file, the one labeled
          "open". This may not work under Catalina.

	- [TightVNC](https://tightvnc.com) will work on most hosts, as it uses Java. In my
      (BPH) experience it is slower.

  - **Note for Windows Subsystem for Linux** you will also need besides a VNC viewer:
    - [X windows for Windows](https://sourceforge.net/projects/xming/)
    - [VcXsrc](https://sourceforge.net/projects/vcxsrv/)

      After installing both:
      - Set the display variable in terminal with "export DISPLAY=$(awk '/nameserver / {print $2; exit}' /etc/resolv.conf 2>/dev/null):0"
      - Start VcXsrv by executing the Xlaunch executable.  On the window where you can select options ("Extra settings") check the box for "Disable access control" and enter "-ac" in the "Additional parameters for VcXsrv" text box.
      - Launch xterm from your WSL terminal with "xterm"


- Install VPN client
  - **For macOS** [Tunnelblick](https://tunnelblick.net/) by
    downloading latest stable release
  - From source
	[OpenVPN](https://openvpn.net/community-downloads/)
  - **Windows Subsystem for Linux**
  [OpenVPN](https://openvpn.net/client-connect-vpn-for-windows/)
  - **For Linux** on Ubuntu flavors
```
apt install openvpn
apt install network-manager-openvpn
apt install network-manager-openvpn-gnome
```


  - On Ubuntu, a way to install the VPN is to run the command below. **Note** you still have to start it, but this will setup everything.
```
nmcli connection import type openvpn file <file.ovpn>
```
  This can also be installed using the graphic user interface. Ubuntu has a system control icon, it looks like a square connected to two other squares below it and is in the upper right. Clicking on that will give a settings option. Click on settings and networking to go to the NetworkManager. That will let you add a file for the VPN configuration. There is an important change that must be made to the file's setup, see below. Without that change, activating the VPN will eliminate the network connection entirely.


- Install miniconda/Anaconda python3
  - Download from : https://docs.conda.io/en/latest/miniconda.html
  - Or download and run the latest installer: https://www.anaconda.com/distribution/
  - **Note** If you have Anaconda or miniconda for Python 2, make sure you install Anaconda or miniconda for Python 3 separately!
  - Add python3 to user path (example below for ~/.bashrc with typical python install path):

      The first is for the macOS and the second is an example for Linux.


```
export PATH=/Users/MyNAME/miniconda3/bin:$PATH
```




```
export PATH=/home/MyNAME/miniconda3 bin:$PATH
```

## Download and Install Lick Remote Observing software

To retrieve the software, you can download it or clone it using git.


- [Click here to download the software as a zipfile](https://github.com/bpholden/lickRemoteObserving/archive/refs/tags/v1.36.zip)


- To clone this project from github:
```
cd ~
git clone https://github.com/bpholden/lickRemoteObserving
cd ~/lickRemoteObserving
```

Once you have downloaded the software:


- If you have NOT installed the Keck remote observing software, create a KRO [conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/environments.html) using the provided environment.yaml file:
```
cd ~/lickRemoteObserving
conda env create -f environment.yaml
```

- If you HAVE installed the Keck remote observing software, you can use that conda environment with this set of scripts.

- Create configuration file:
 - If you have a Mac and have used our software suggestions
```
cp mac_config.yaml local_config.yaml
````

 - If you have a Linux host and have used our software suggestions
 ```
 cp linux_config.yaml local_config.yaml
 ````

 - If you want to double check, copy ```lick_vnc_config.yaml``` and follow the directions inside.

 ```
 cp lick_vnc_config.yaml local_config.yaml
 ```


- (optional) Add VNC start script to path:
```
export PATH=/home/observer/lickRemoteObserving:$PATH
```

## Configure Lick Remote Observing software

Edit the configuration file  ```local_config.yaml```.  Read the comments in the
configuration file itself as they can guide you.  You may need to
uncomment (remove the leading `#`) from lines you want to customize.
**Note each line must not have a space at the start!**
```
vncviewer : 'vncviewer'
```

- **Configure OpenVPN:**
Obtain the OpenVPN (ovpn) file for your schedule observing run.

  - **For macOS**: Open the Tunnelblick and click on the
    ```VPN Details``` menu item. When the window for Tunnelblick
    opens, click on the Configurations tab at the top, it is in the
    upper left. 	Using the Finder, drag the tblk file into your
    configurations list on the left. It will ask if you want this
    installed for everyone or only you, select "Me". The hit the
    connect button to start the VPN.

  - **For Linux**: Install the certificate using appropriate
	commands, or the NetworkManager GUI.  If NetworkManager is used it will
	by default try to route all traffic through the VPN. That will prevent network
	connections to anywhere other than the MH VNC hosts, which means no Zoom,
	no browser, no other network traffic. Tell NetworkManager not to
	route all traffic through the VPN using a command like the
	examples below

	```nmcli connection modify Nickel20200507 ipv4.never-default yes```

	or

	```nmcli connection modify ShaneB20200521--P1D ipv4.never-default yes```

	where the ```Nickel``` or ```Shane``` word is the name of the OpenVPN config file.
	Alternatively this can be accomplished using the NetworkManager editor
	GUI during or after the import of the OpenVPN config file by going to

	```IPv4 Settings > Routes... > Use this connection only for resources on its network```

	checking that checkbox, pressing ```OK```, and pressing ```Save```. After this the
	new OpenVPN configuration should appear in the NetworkManager widget as
	one of the ```VPN Connections``` If you have the option to make
	DNS and Routes Automatic, leave those ON.

- **Configure Local VNC Viewer Software:** This is where one sets
  `vncviewer` with the path and executable for the local VNC viewer
  client (for Linux we recommend TigerVNC as the most compatible with our
  system).  Some VNC viewers (such as the built in macOS one) may need
  a prefix such as `vnc://` which can be set via the `vncprefix`
  value.  Options which should be passed to the vncviewer application
  are set in the `vncargs` value (defaults should be good for Tiger
  VNC). This goes in the file ```local_config.yaml```

    - **Important:** IF and ONLY IF you are using TigerVNC, make sure you have configured your client **not** to resize the sessions (see the note above).
    - **On Linux:** (optional) Save VNC session password (not available on macOS):
        - NOTE: This is for the final password prompt for each VNC window.
        - Run the `vncpasswd` command line utility and note where it saves the VNC password file.
        - Edit `local_config.yaml` to include the password file as a VNC start option:
            ```
            vncargs: '-passwd=/home/observer/.vnc/passwd',
            ```
	- **On MacOS** (optional) If you use the MacOS builtin VNC
          viewer, you can optionally save the password by clicking the
          box that says "Remember Password"


- **Soundplay Configuration:** For compatible systems, uncomment the
  `soundplayer` line to specify which compiled executable for
  soundplay to use.  Other operating systems sometimes need other
  soundplay versions, contact `holden@ucolick.org` for help configuring
  this value.  Also, if you local machine's path to the `aplay`
  executable is non-standard, specify that in the `aplay` value.


-   If your system is not compatible with soundplay, or if you do not want it to have sounds, add a line to your `local_config.yaml` file: `nosound: True,` to avoid starting sounds.  This is important
for sites which are using multiple computers for each set of VNC   sessions.  Choose one to handle sounds, and set the `nosound:  True,` option for the other.


# Test your connection to Lick


From the directory where the Lick VNC software is installed
(e.g. `~/lickRemoteObserving/`), run ```test_connection```
**This will only work ONCE A VPN connection is made.**

```
cd ~/lickRemoteObserving
./test_connection
```

It should print out a report which indicates that all four
tests passed. Make sure there are no test failures.

If there are test failures, email your log file to `holden@ucolick.org`.
Verbose debug information is logged to the `lickRemoteObserving/logs/`
folder.  Log files are created based on the UTC date.


# Run the VNC launch script

From the command line, cd into your install directory and run
`start_lick_viewers` followed by the name of the instrument account
assigned for your observing night (ie `shane`, `nickel`).  Running the
script without options will start 6 VNC sessions for the Kast and the
soundplayer. Additionally, you should see a command line menu with
more options once you have started the script.:

```
cd ~/lickRemoteObserving
./start_lick_viewers [shane or nickel]
```

To get help on available command line options:
```
./start_lick_viewers --help
```

That will output the following:
```
usage: lick_vnc_launcher.py [-h] [--authonly] [--nosound] [--test]
                            [--tags TAGS] [--check CHECK] [--novpn]
                            [--viewonly] [-c CONFIG]
                            [account]

Lick VNC Launcher (v1.26). This program is used by approved Lick Remote
Observing sites to launch VNC sessions for the specified telescope account.
For help or information on how to configure the code, please see the included
README.md file or email holden@ucolick.org

positional arguments:
  account               The user account.

optional arguments:
  -h, --help            show this help message and exit
  --authonly            Authenticate only
  --nosound             Skip start of soundplay application.
  --test                Run only tests
  --tags TAGS           Soundplay tags, defaults to ":1,:2,:3,:4,:5,:6"
  --check CHECK         How to check for open ports.
  --novpn               Turn off VPN check to allow the software to run
                        without a VPN.
  --viewonly            Runs the VNC viewer in view only mode
  -c CONFIG, --config CONFIG
                        Path to local configuration file.
```

**NOTE:** Be sure to exit the script by using the 'q' quit option or
  control-c to ensure all VNC processes, SSH tunnels, and
  authentication are terminated properly.


# Troubleshooting and common problems

- Older version of Anaconda or miniconda can cause a problem.
- Make sure that there are no spaces at the start of lines in the local_config.yaml file.

Verbose debug information is logged to the `lickRemoteObserving/logs/` folder.  Log files are created based on the UTC date.

If you need assistance, please email `holden@ucolick.org` and attach the most recent log file from the logs folder.
