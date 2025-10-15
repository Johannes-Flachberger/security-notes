tags: #type/theory

---
# FTP
file transfer protocol
default ports: 20 - data, 21 control 
operates on 2 channels/ports: control channel for commands & data channel for data
-   very efficient
- credentials and commands are sent in cleartext!
### 2 modes:
**active:** data is sent over a separate channel originating from the FTP server’s port 20
**passive:** data is sent over a separate channel originating from an FTP client’s port above port number 1023

## Usage
`ftp [ip]`
**in ftp shell:**
output content of file:
`get [filename] -` 
`STAT` show some info
`SYST`: show sytem type
`TYPE A`: use ASCII for file transfer
`TYPE I`: use binary for file transfer

[https://www.exploit-db.com/exploits/20745](https://www.exploit-db.com/exploits/20745)

  
