import requests
import pandas as pd
import numpy as np
import datetime

def getBoosterVersion(data):
    for x in data['rocket']:
       if x:
        response = requests.get("https://api.spacexdata.com/v4/rockets/"+str(x), verify=r'C:\Users\c057468\Desktop\Nova pasta (3)\testes\capstone\Cisco Umbrella Root CA.crt').json()
        BoosterVersion.append(response['name'])

def getLaunchSite(data):
    for x in data['launchpad']:
       if x:
         response = requests.get("https://api.spacexdata.com/v4/launchpads/"+str(x), verify=r'C:\Users\c057468\Desktop\Nova pasta (3)\testes\capstone\Cisco Umbrella Root CA.crt').json()
         Longitude.append(response['longitude'])
         Latitude.append(response['latitude'])
         LaunchSite.append(response['name'])
def getPayloadData(data):
    for load in data['payloads']:
       if load:
        response = requests.get("https://api.spacexdata.com/v4/payloads/"+load, verify=r'C:\Users\c057468\Desktop\Nova pasta (3)\testes\capstone\Cisco Umbrella Root CA.crt').json()
        PayloadMass.append(response['mass_kg'])
        Orbit.append(response['orbit'])
def getCoreData(data):
    for core in data['cores']:
            if core['core'] != None:
                response = requests.get("https://api.spacexdata.com/v4/cores/"+core['core'], verify=r'C:\Users\c057468\Desktop\Nova pasta (3)\testes\capstone\Cisco Umbrella Root CA.crt').json()
                Block.append(response['block'])
                ReusedCount.append(response['reuse_count'])
                Serial.append(response['serial'])
            else:
                Block.append(None)
                ReusedCount.append(None)
                Serial.append(None)
            Outcome.append(str(core['landing_success'])+' '+str(core['landing_type']))
            Flights.append(core['flight'])
            GridFins.append(core['gridfins'])
            Reused.append(core['reused'])
            Legs.append(core['legs'])
            LandingPad.append(core['landpad'])

BoosterVersion = []
PayloadMass = []
Orbit = []
LaunchSite = []
Outcome = []
Flights = []
GridFins = []
Reused = []
Legs = []
LandingPad = []
Block = []
ReusedCount = []
Serial = []
Longitude = []
Latitude = []

pd.set_option('display.max_columns', None)
pd.set_option('display.max_colwidth', None)
spacex_url="https://api.spacexdata.com/v4/launches/past"
response = requests.get(spacex_url, verify=r'C:\Users\c057468\Desktop\Nova pasta (3)\testes\capstone\Cisco Umbrella Root CA.crt')
json=response.json()
json_normalize=pd.json_normalize(json)
data=pd.DataFrame(json_normalize)
data=data[['rocket', 'payloads', 'launchpad', 'cores', 'flight_number', 'date_utc']]
data = data[data['cores'].map(len)==1]
data = data[data['payloads'].map(len)==1]
data['cores'] = data['cores'].map(lambda x : x[0])
data['payloads'] = data['payloads'].map(lambda x : x[0])
data['date'] = pd.to_datetime(data['date_utc']).dt.date
data = data[data['date'] <= datetime.date(2020, 11, 13)]
getBoosterVersion(data)
getLaunchSite(data)
getPayloadData(data)
getCoreData(data)
launch_dict = {'FlightNumber': list(data['flight_number']),
'Date': list(data['date']),
'BoosterVersion':BoosterVersion,
'PayloadMass':PayloadMass,
'Orbit':Orbit,
'LaunchSite':LaunchSite,
'Outcome':Outcome,
'Flights':Flights,
'GridFins':GridFins,
'Reused':Reused,
'Legs':Legs,
'LandingPad':LandingPad,
'Block':Block,
'ReusedCount':ReusedCount,
'Serial':Serial,
'Longitude': Longitude,
'Latitude': Latitude}
data=pd.DataFrame.from_dict(launch_dict)
data_falcon9 = data[data['BoosterVersion']=='Falcon 9']
data_falcon9.loc[:,'FlightNumber'] = list(range(1, data_falcon9.shape[0]+1))
data_falcon9.isnull().sum()
data_falcon9['PayloadMass'] = data_falcon9['PayloadMass'].fillna(data_falcon9['PayloadMass'].mean())




