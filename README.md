# Port Scanner

A command-line tool written in Python that scans a target IP address for open ports. Built as a personal project to explore basic network security and reconnaissance concepts alongside learning Python.

## ⚠️ Important: Use responsibly

This tool should only ever be run against devices and networks you own or have explicit permission to test — such as your own PC (`127.0.0.1`) or your own home network. Scanning devices you don't own or don't have permission to test may be illegal, even without malicious intent.

## What it does

- Attempts a connection to each port in a given range on a target IP
- Reports which ports are open
- Gives a summary once the scan completes

## Why I built this

I'm learning Python and interested in cybersecurity, so I wanted a hands-on introduction to network reconnaissance — one of the first steps in real-world security assessments. Port scanning helps reveal what services are running on a machine, which is useful both for defenders (auditing their own exposure) and for understanding how attackers gather information about a target.

## How it works

- `scan_port(ip, port)` attempts a TCP connection to a single port using Python's built-in `socket` library, with a short timeout so scanning doesn't stall on unresponsive ports
- `scan_range(ip, start_port, end_port)` loops through a range of ports, calling `scan_port` on each one and collecting the open ones
- `main()` prompts the user for a target IP and port range, then runs the scan

## Running it

```
python port_scanner.py
```

Follow the prompts to enter a target IP (use `127.0.0.1` to scan your own machine) and a port range.

## Example

Scanning `127.0.0.1` on a Windows machine often reveals ports like:
- **135** — Microsoft RPC, used internally by Windows services
- **445** — SMB, used for file/printer sharing (historically a common target for exploits when exposed to public networks)

This is a good demonstration of why port scanning matters: even scanning your own machine reveals real information about what's installed and running.

## Limitations

- Only supports TCP scanning (not UDP)
- Scans sequentially, so large port ranges can take a while due to per-port timeouts
- Does not attempt to identify what service is running on an open port (no banner grabbing)

