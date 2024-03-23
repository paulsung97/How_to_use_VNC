# How_to_use_VNC
Using a remote server with VNC

# Setting Up TightVNC Server on Ubuntu GPU Server

This guide provides a step-by-step approach to installing and configuring the TightVNC server on an Ubuntu GPU server. Follow these instructions to enable remote desktop access to your server.

## Step 1: Install TightVNC Server

Open the terminal on your Ubuntu GPU server and execute the following commands to install TightVNC Server:

```bash
sudo apt update
sudo apt install tightvncserver
```

## Step 2: Configure VNC Server

To configure the VNC server for the first time, run:

```bash
tightvncserver
```

Upon the first launch, you will be prompted to set a password for accessing the VNC server. Enter your desired password and proceed with the confirmation. After setting up the password, the VNC server will start. Each client connection will initiate a new VNC display.

The default port for the VNC server is 5900. When asked, "Would you like to enter a view-only password (y/n)?", select 'n' to ensure full interaction capabilities with the server. Choosing 'y' would restrict you to view-only mode, disabling interaction.

## Step 3: Configure Firewall

By default, Ubuntu's firewall blocks port 5900, which is used by the VNC server. Open this port by running:

```bash
sudo ufw allow 5901/tcp
```

## Step 4: Connect Using a VNC Client

Next, connect to your server using a VNC client. Here’s how:

1. Download and install RealVNC for your operating system from [RealVNC Download Page](https://www.realvnc.com/en/connect/download/viewer/).
2. Create an account or log in if you already have one.
3. Launch the installed RealVNC Viewer and log in.

To connect, enter your server's IP address followed by ':5901' in the connect field.
<img width="717" alt="image" src="https://github.com/paulsung97/How_to_use_VNC/assets/63456050/03a95633-8e9d-4e87-935d-2990757cdafa">
## Step 5: Initial Connection and Script Modification

Upon connecting for the first time, you might encounter a grey screen. To resolve this, execute the following command in your server terminal to kill the current VNC session:

<img width="542" alt="image" src="https://github.com/paulsung97/How_to_use_VNC/assets/63456050/b4858d69-f6fa-4065-bb4c-fd86e0579e30">

```bash
vncserver -kill :1
```

Then, edit the `~/.vnc/xstartup` script:

```bash
vi ~/.vnc/xstartup
```

Replace its contents with the following script:

```bash
#!/bin/sh
def
export XKL_XMODMAP_DISABLE=1
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
```

Save and exit by typing `:wq`. Now, restart the VNC server with the desired geometry:

```bash
vncserver :1 -geometry 1920x1080
```

This setup allows you to interact with your server using a graphical interface.

## Troubleshooting

If you encounter issues or the VNC server is not listening on the expected port, use this command to check:

```bash
sudo netstat -tuln | grep 5901
```

This command checks if the VNC server is listening on port 5900. If there's a need to switch to port 5901 due to any issues, remember to adjust the firewall settings accordingly.

---

Feel free to adapt this template to match your specific needs or preferences!
