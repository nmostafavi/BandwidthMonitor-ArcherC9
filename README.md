# NetworkStatistics-ArcherC9
Fetch network usage data from TP-LINK Archer C9 router via CLI

## About
This script will fetch network traffic statistics from the web interface of the TP-LINK Archer C9 router and either save them to disk or display them for your perusal. 

I have written this script in order to compare my internally-gathered bandwidth usage statistics against measurements provided by my ISP. Please keep in mind that the data gathered likely includes all LAN traffic, and sadly may not be fully accurate for purposes of monitoring WAN throughput.

## Requirements
Statistics collection must be enabled on the router, under `Advanced` > `System Tools` > `Statistics`. As a requirement of statistics collection, the router must have the "NAT Boost" setting turned off, under `Advanced` > `NAT Boost`.

This script is written for Python 3. To install required libraries, run: 
```python3 -m pip install -r requirements.txt```

## Arguments
```
usage: stats.py [-h] [-a ADDRESS] [-u USERNAME] [-p PASSWORD] [-o OUTFILE]

optional arguments:
  -h, --help            show this help message and exit
  -a ADDRESS, --address ADDRESS
                        Host address (IP or hostname) of the router. (default: '192.168.1.1')
  -u USERNAME, --username USERNAME
                        Username used to log into the router. (default: 'admin')
  -p PASSWORD, --password PASSWORD
                        Password used to log into the router. (default: 'admin')
  -o OUTFILE, --outfile OUTFILE
                        Destination file path to write the latest router statistics snapshot
                        to.
```

## How to use
Simply run the script providing your router's address, username, and password provided as arguments, e.g. `./stats.py -a 192.168.1.1 -u root -p password`.

A quick summary of throughput statistics will be printed, in ascending order:
```
48-58-E8-BA-60-26: 1,710 MB
49-2F-37-0B-9D-B6: 977 MB
FE-B7-18-E6-5F-FE: 868 MB
2E-91-09-E5-75-03: 802 MB
...
Total: 8,917 MB
```

If an output file path is specified, the script will silently generate a JSON file containing a more comprehensive summary of bytes transferred. If no host address, username, or password is specified, the default values for the router will be used (i.e. `192.168.1.1`, `admin`/`admin`).
