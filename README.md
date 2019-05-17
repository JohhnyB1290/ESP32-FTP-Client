# ESP32-FTP-Client
## Description
Set of routines that implement the FTP Client for ESP32. They allow to create and access remote files. Based on [ftplib V4.0-1](https://nbpfaus.net/~pfau/ftplib/).

## How to
This library uses esp32 <sys/socket.h> and vfs. But it can be easily ported to LwIp sockets and ChaN FatFs.
All methods implemented in FtpClient struct as pointers to static functions.</br>
Have only one function getFtpClient, which returns pointer to FtpClient struct. </br>
Besides this you can use [working documentation of ftplib](https://nbpfaus.net/~pfau/ftplib/ftplib.html).</br>
For debug purposes you can change **FTP_CLIENT_DEBUG** define in FtpClient.h to **1**(not print cmd/response) or **2**(print all).

##### Example
```
int main(void)
{
    static NetBuf_t* ftpClientNetBuf = NULL;
    FtpClient* ftpClient = getFtpClient();
    ftpClient->ftpClientConnect("127.0.0.1", 21, &ftpClientNetBuf);
    ftpClient->ftpClientLogin("user","password", ftpClientNetBuf);
    ftpClient->ftpClientGet("/sdcard/test.txt", "test.txt",
                FTP_CLIENT_BINARY, ftpClientNetBuf);
    ftpClient->ftpClientQuit(ftpClientNetBuf);
}
```