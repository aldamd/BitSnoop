# BitSnoop
BitSnoop is a lightweight Python tool for parsing BitTorrent traffic from a packet capture (`.pcap` / `.pcapng`) and reconstructing the transmitted files. Created for CTF use, it identifies BitTorrent piece messages, reassembles the payloads, detects file types, and writes them to disk.

## Features
- Parses BitTorrent `piece` messages from a pcap
- Reconstructs transferred files by socket mapping
- Auto-detects file types
- Writes recovered files to disk with source/destination info in the filename

## Requirements
- Python 3.7+
- [pyshark](https://github.com/KimiNewt/pyshark)
- [python-magic](https://github.com/ahupp/python-magic)
- Wireshark / TShark must be installed and available in `$PATH`  
Install dependencies with:
```sh
pip install pyshark python-magic
```

## Usage
```sh
./bitsnoop <pcap_file>
```
Example:
```sh
❯ ./bitsnoop sample.pcapng
[-] Reading sample.pcapng...
[-] Packets processed: 358
[+] Found: 34.10.241.248:6881 -> 192.168.1.23:44487 Type: pdf
```
Recovered files will be saved in the current directory, with filenames based on the IP/port pairs.

## Notes
- Only BitTorrent piece messages are extracted. Other BitTorrent messages are ignored.
- Large captures may take time to process, progress is printed live.
