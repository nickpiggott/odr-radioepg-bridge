ODR Bridge EPG
==============

Creates a DAB EPG bitstream directly from the ODR multiplex configuration file, using RadioDNS to lookup SI and PI documents.

# Dependencies

* [python-hybridspi](https://github.com/opendigitalradio/python-hybridspi)
* [odr-radiodns-bridge](https://github.com/opendigitalradio/odr-radiodns-bridge)
* [python-dabmot](https://github.com/opendigitalradio/python-dabmot)
* [python-mot-epg](https://github.com/opendigitalradio/python-mot-epg)
* [python-dabmsc](https://github.com/opendigitalradio/python-dabmsc)
* [isodate](https://pypi.python.org/pypi/isodate)
* [bitarray](https://pypi.python.org/pypi/bitarray)
* [crcmod](https://pypi.python.org/pypi/crcmod)

# Usage

```
usage: generate-epg [-h] [-o OUTPUT] [-X] [-p bytes] [-a address] [-d DAYS] [-D] [-c filename] f

Encodes an EPG bitstream for services in a multiplex configuration file

positional arguments:
  f           multiplex configuration file
              the configuration file must be in the Boost format
              configuration files in JSON format are currently not supported

optional arguments:
  -h, --help  show this help message and exit
  -o OUTPUT   output bitstream file (default output.dat)
  -X          turn debug on
  -p          size of data packets in bytes (default 96)
  -a          packet address (default 1)
  -d DAYS     number of days ahead to encode schedule files (default 2)
  -D          output as data groups, not packets
  -c          filename of a CSV file containing client IDs (see below)
```

# Client ID
Some providers of RadioDNS SI information control access through use of a Client ID (a kind of API key).
This Client ID must be passed as part of any request for SI or PI files; without it the request may fail
either with a 401 (Unauthorized) error, silently or by returning a truncated (but valid) SI / PI document.

Client IDs are associated with the FQDN (Full Qualified Domain Name) of the provider of the SI / PI files.
In order to pass Client IDs to the Service Provider when making a request, you can provide the filename
of a csv file, which contains one or more lines in the format
{fqdn},{ClientId}

for example:
```
radiodns.example.com,bf8f7abf-7194-4222-ab1e-3329aae254c9
```

If Authorization of a Client ID fails, odr-radioepg-bridge will move onto the next service silently. 
The error will not be reported, and processing will not stop.

To get a Client ID, you'll need to approach the radio station or their service provider directly.
Client IDs are not issued or managed by RadioDNS or OpenDigitalRadio.

