# IP-location
## Python - This is python code is written to find location of IP. The details of the IP is fetching from the site "ipstack.com". We need an API key to fetch the details from "ipstack.com" and it is easy to get a free API key from the domain by just entering your info. The code will take the values of IP and key from the command line  and give you the location. I have used the module argparse in python for command line argument and requests module to get the details from "ipstack.com"

```python
import argparse
import requests
import json

parser = argparse.ArgumentParser()

parser.add_argument('-i',
                               dest = 'ip',
                               help = 'IP required to check the details',
                               required = True)
parser.add_argument('-k',
                               dest = 'key',
                               help = 'Key to access the ipstack',
                               required = True)

arguments = parser.parse_args()

ip = arguments.ip
key = arguments.key

try:
    url = 'http://api.ipstack.com/{}?access_key={}'.format(ip,key)
    response = requests.get(url)
    geodata = response.json()
    country_name = geodata['country_name']
    country_code = geodata['country_code']
    print('The provided IP is {} and the location is :{:10} {}'.format(ip,country_name,country_code))
except:
    print('Please enter the valid credentials')
```

## The usage of this code and the sample output is provided below.

- ubuntu@ip-172-**** python3 location.py -i 8.8.8.8 -k 604a43d7a0a1971161d9a6da7194a3c2
The provided IP is 8.8.8.8 and the location is :United States US

- ubuntu@ip-172-****:~$ python3 location.py -i 1.2.3.4 -k 604a43d7a0a1971161d9a6da7194a3c2
The provided IP is 1.2.3.4 and the location is :United States US

- ubuntu@ip-172-****:~$ python3 location.py -i 192.168.1.1 -k 604a43d7a0a1971161d9a6da7194a3c2
Please enter the valid credentials
