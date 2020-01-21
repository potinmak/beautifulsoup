# beautifulsoup
Python Data Structure Assignment: Extracting Data from XML
import urllib.request, urllib.parse, urllib.error
import xml.etree.ElementTree as ET
import ssl

api_key = False
# If you have a Google Places API key, enter it here
# api_key = 'AIzaSy___IDByT70'
# https://developers.google.com/maps/documentation/geocoding/intro

if api_key is False:
    api_key = 42
    serviceurl = 'http://py4e-data.dr-chuck.net/xml?'
else :
    serviceurl = 'https://maps.googleapis.com/maps/api/geocode/xml?'

# Ignore SSL certificate errors
ctx = ssl.create_default_context()
ctx.check_hostname = False
ctx.verify_mode = ssl.CERT_NONE
#http://python-data.dr-chuck.net/comments_42.xml

url = input('Enter Location: ')
print('Retrieving', url)
handle = urllib.request.urlopen(url).read()
print('Retrieved', len(handle), 'characters')


tree = ET.fromstring(handle)
cc = tree.findall('.//count')
print('Count:', len(cc))
sum_of_numbers = list()

for c in cc: 
     sum_of_numbers.append(int(c.text))
print('Sum:', sum(sum_of_numbers))
