- The Drone uses Arch armv7h OS.
- Doesn't currently have a UI, think of xcfe as Desktop environment.
- Connects to any previously known wifi automatically on boot.
> please use `iwctl` (also called iwd) to connect to a new wifi on first start, not `netctl`, `network-manager` or `wifi-menu`.

- Ip address of wifi ssh is: 192.168.113.30
- Note: Only connects over private network like mobile hotspot and not public network like UPESNET.
- there are two accounts available:
	- account name: alarm, password: wrise
	- account name: root, password: root
- always use the first account.
- format of remoting is: open terminal or cmd, and assuming you have ssh installed, run ` ssh alarm@192.168.113.30` .
- Then it will ask for password, type the password KEEP IN MIND the password might not be shown as you type, just type the password and press enter. 