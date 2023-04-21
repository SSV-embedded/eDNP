# eDNP/8331-EK: First Steps with the Evaluation Kit (EK) 

An eDNP/8331-EK consists of an MB/941 carrier board and various accessory components. These include a 110/230 VAC to 24 VDC EU plug-in power supply, an RS232 interface cable and an Ethernet LAN connection cable. The 40-pin DIL (dual in-line) socket of the MB/941 contains a DNP/8331, the physical version of the eDNP/8331 "virtual" system-on-module (SoM). 

For the evaluation kit commissioning, only an RS232 and LAN connection to a PC must be established and the 24 VDC supply voltage must be provided.

On the back of the MB/941 there is a label sticker with individual data. These are required for logging into the different eDNP/8331-EK firmware user interfaces and for activating the Over-the-Air (OTA) software update capabilities of the evaluation kit.  

![Overview](https://ssv-comm.de/forum/bilder/8331EK-overview.jpg)

The commissioning of the eDNP/8331-EK is relatively simple. Since a microSD card with the bootable firmware is pre-installed in the DNP/8331-SD card holder, it is only necessary to provide a 24 VDC supply voltage using the plug-in power supply from the scope of delivery. In total, there are four remote access possibilities ex works ready to use: One command-line Linux user interface via RS232 (serial console session) or Ethernet LAN (SSH client session) and only via Ethernet LAN a file transfer interface (SFTP client session) and one web-based configuration interface (webbrowser session with SSV/WebUI).  

## Serial Console Session

Use of the serial console requires an RS232 interface connection between the eDNP/8331-EK board and the user's PC. The setup parameters **115,200 bps, 8N1** apply to this connection. Furthermore, terminal emulator software such as Tera Term or PuTTY is required on the PC (see also https://en.wikipedia.org/wiki/Tera_Term).

![Overview](https://ssv-comm.de/forum/bilder/8331EK-Serial.png)

To request the eDNP/8331 Linux operating system to issue a login prompt in the terminal emulator window, first press the PC's Enter key once. Then you can log in with user name and password. The two entries required for this login can be found on a label sticker on the back of the eDNP/8331-EK board.

After a successful login with username and password, any eDNP/8331 Debian Linux commands can be executed via command line (Linux CLI) within the serial console session.

## SSH Client Session

Analogous to the serial console session, an SSH client session via Ethernet LAN is also possible using the factory default IP address **192.168.0.126** of the eDNP/8331-EK board. The integrated SSH client from Tera Term can be used for this purpose, for example.

An SSH client session also requires a login first. The two entries required for this can also be found on a label sticker on the back of the eDNP/8331-EK board.

![Overview](https://ssv-comm.de/forum/bilder/8331EK-SSH.png)

After a successful login with username and password, any eDNP/8331 Debian Linux commands can be executed via command line (Linux CLI) within the SSH client session.

## SFTP Client Session

In addition to a Linux Command Line Interface (Linux CLI) usable via RS232 or LAN interface connection, the eDNP/8331 Linux provides a SFTP server to transfer arbitrary directories and files from the PC to the Linux file system via Ethernet LAN only using the factory default IP address **192.168.0.126**. To use this service, a SFTP client, such as FileZilla, is required on the PC (see https://en.wikipedia.org/wiki/FileZilla).

![Overview](https://ssv-comm.de/forum/bilder/8331EK-SFTP.png)

A SFTP client session also requires a login first. The two entries required for this can also be found on a label sticker on the back of the eDNP/8331-EK board.

After establishing a SFTP connection with a successful login, directories and files can be transferred in both directions, i.e. from the PC to the eDNP/8331 Linux file system and vice versa.

## Webrowser Session (SSV/WebUI)

Another possibility for Ethernet LAN-based user access is provided by the SSV/WebUI and the eDNP/8331 embedded web server provided for this purpose at http://192.168.0.126:7777. This user interface can be accessed from any computer using a web browser.

![Overview](https://ssv-comm.de/forum/bilder/8331EK-WUI.png)

Immediately after the first access, a login web page is displayed. Here, a user name plus password must first be entered in order to start an SSV/WebUI session. The two entries required for this can also be found on a label sticker on the back of the eDNP/8331-EK board.

## Python "Hello World!"

A Python 3 runtime is included in the Linux operating system of the eDNP/8331. It is therefore recommended to use a PC workstation with Visual Studio Code (VSC or VS Code, see https://en.wikipedia.org/wiki/Visual_Studio_Code) as development computer, edit the Python source code files on the PC, transfer them via SFTP to the eDNP/8331 Linux file system and execute them there.

![Overview](https://ssv-comm.de/forum/bilder/8331EK-VSC.png)

Visual Studio Code can be extended relatively easily via plug-ins (VSC extensions). For example, it is possible to integrate one SSH and one SFTP client into VSC. This allows an SSH client session to the eDNP/8331-EK board in parallel to the code editor window (see terminal window in the figure above of this text). Furthermore, with one mouse click the SFTP file transfer of the Python code from the VSC editor window to the eDNP/8331 Linux file system is possible.

## Over-the-Air (OTA) Software Updates

To ensure the necessary cybersecurity in a networked eDNP/8331 application, a continuous over-the-air (OTA) software update process with the highest possible degree of automation is required. To evaluate the technical details and interrelationships, the eDNP/8331-EK offers an easy entry with the help of the SSV Secure Device Update (SDU) infrastructure functions.

![Overview](https://ssv-comm.de/forum/bilder/8331EK-OTA.jpg)

The central function module for eDNP/8331 OTA software updates is an SDU/OTA server in the Internet. On this server, the software maintainer in charge can place an object signed with the help of a public key infrastructure (PKI), which is automatically downloaded by an eDNP/8331 SDU update agent and, after a successful integrity check, added to the local software installation.

## Connectors, Slots and Wireless Modem

Due to the different connectors of the MB/941 carrier board, there are numerous possibilities to evaluate own eDNP/8331 IoT application scenarios. The following figure provides an overview and further details on the individual functions.

![Overview](https://ssv-comm.de/forum/bilder/8331EK-explore.jpg)

**(1)** SIM card slot for the miniPCIe slot **(6)**.

**(2)** System IO: 1x I2C, 1x UART (TTL interface with RXD, TXD). I2C is suitable as an interface for various sensors, actuators, etc. The two I2C signals can alternatively be used as GPIOs. The UART interface is used for the integration of internal subsystems.

**(3)** DNP/8331 with A/B boot loader, Debian operating system, SSV/WebUI, Python runtime environment (DNP/8331-EVA firmware).

**(4)** 1x 10/100 Mbps Ethernet LAN with 1x status LED (Link, Activity). Support through an extensive TCP/IP protocol stack. User access to the operating system and individual firmware functions. Connection to external systems (e.g. via Modbus TCP, OPC UA, RFC 1006, MQTT and many others).

**(5)** 1x UART (RS232 interface with TXD, RXD, RTS, CTS). General purpose RS232 serial I/O for connections to other subsystems.

**(6)** 1x miniPCIe slot for wireless wide area network (WWAN) modem modules (e.g. 4G, LTE Cat M1, NB-IoT modem, IoT satellite connections).

**(7)** 2x LED, one of them controllable by software, the other LED indicates the power-on state.

**(8)** 24 VDC power supply, 1x UART (RS485 interface, e. g. for connections to external Modbus RTU devices).

**(9)** Option: Wireless modem module for miniPCIe slot **(6)**. Used to connect the eDNP/8331 to Wireless Wide Area Networks (WWANs). 

[(e)DNP/8331 Hardware Reference](https://www.ssv-embedded.de/doks/manuals/hr_dnp8331_en.pdf)

[MB/941 Hardware Reference](https://www.ssv-embedded.de/doks/manuals/hr_mb941_en.pdf)
