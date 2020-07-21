ODR Bridge EPG
==============

Creates a DAB EPG bitstream directly from the ODR multiplex configuration file, using RadioDNS to lookup SI and PI documents.

**This is a experimental version to reduce the sizes of logo image files to below 16kbytes**
It requires Pillow for image handling, in addition to the usual dependencies.

# Dependencies

* [python-hybridspi](https://github.com/nickpiggott/python-hybridspi)
* [odr-radiodns-bridge](https://github.com/nickpiggott/odr-radiodns-bridge)
* [python-mot](https://github.com/GlobalRadio/python-dabmot)
* [python-mot-epg](https://github.com/GlobalRadio/python-mot-epg)
* [python-msc](https://github.com/nickpiggott/python-dabmsc)
* [isodate](https://pypi.python.org/pypi/isodate)
* [bitarray](https://pypi.python.org/pypi/bitarray)
* [crcmod](https://pypi.python.org/pypi/crcmod)
* [Pillow](https://pypi.python.org/pypi/pillow)

# Usage

```
usage: generate-epg [-h] [-o OUTPUT] [-X] [-p bytes] [-a address] [-d DAYS] [-D] f

Encodes an EPG bitstream for services in a multiplex configuration file

positional arguments:
  f           multiplex configuration file

optional arguments:
  -h, --help  show this help message and exit
  -o OUTPUT   output bitstream file (default output.dat)
  -X          turn debug on
  -p          size of data packets in bytes (default 96)
  -a          packet address (default 1)
  -d DAYS     number of days ahead to encode schedule files (default 2)
  -D          output as data groups, not packets
```

