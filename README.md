# Observable Trends and Description:

## 1. LATITUDE vs MAX TEMPERATURE
Most of the max temperatures (60-95deg F) are happen around the equator. The lowest temperatures belong to the northern parts of the world.

## 2. LATITUDE vs CLOUDINESS
The cloudiness is pretty evenly spread out all over the world for this day.

## 3. LATITUDE vs HUMIDITY
The evenly spread out cloudiness correlates with the pretty evenly spread out humidity, 30 – 100%, with the ‘dry’ area of 2 – 30% on the Lat 15 – 40 deg.

## 4. LATITUDE vs WIND SPEED
This day is relatively calm everywhere in terms of wind speed, mostly in range of 3 – 15 mph, with some areas of 25 – 40 mph.


```python
# WeatherPy 3/30/2018
# Imports
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import urllib.request
import requests
import json
from config import api_key
from pprint import pprint
from citipy import citipy
from random import uniform
# Set style for plots
plt.style.use("seaborn")
```


```python
url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID="+api_key
```


```python
cities = []
all = pd.DataFrame()

while len(cities) < 500:
    lat = uniform(-90, 90)
    lon = uniform(-180, 180)
    #print(lat, lon)
    city = citipy.nearest_city(lat, lon)
    #print(city.city_name, city.country_code)
    if city.city_name not in cities:
        city_name = city.city_name.replace(" ", "%20")
        weather_city_url = url + "&q=" + city_name + "," + city.country_code
        response = requests.get(weather_city_url).json()
        #print(json.dumps(response, indent=4, sort_keys=True))
        if 'name' in response.keys():
            cities.append(city.city_name)
            city_name = response['name']
            city_id = response['id']
            country = response['sys']['country']
            date = response['dt']
            latitude = response['coord']['lat']
            longtitude = response['coord']['lon']
            temperature = response['main']['temp']
            humidity = response['main']['humidity']
            cloudiness = response['clouds']['all']
            wind = response['wind']['speed']
            print("Processing: ", len(cities), city_name, city_id)
            print(weather_city_url)
            all = all.append([{"City":city_name,
                        "CityID":city_id,
                       "Country":country,
                       "Latitude":latitude,
                       "Longtitude":longtitude,
                       "Date":date,
                       "Cloudiness":cloudiness,
                       "Max Temp":temperature,
                       "Humidity":humidity,
                       "Wind Speed":wind}])
        


```

    Processing:  1 Zhanakorgan 1517323
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zhanakorgan,kz
    Processing:  2 Busselton 2075265
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=busselton,au
    Processing:  3 Vaini 4032243
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vaini,to
    Processing:  4 Thompson 6165406
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=thompson,ca
    Processing:  5 Rikitea 4030556
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rikitea,pf
    Processing:  6 Ornskoldsvik 2686469
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ornskoldsvik,se
    Processing:  7 Ballina 2966778
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ballina,ie
    Processing:  8 Jamestown 3370903
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=jamestown,sh
    Processing:  9 Jauja 3937733
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=jauja,pe
    Processing:  10 Kapaa 5848280
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kapaa,us
    Processing:  11 Khatanga 2022572
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=khatanga,ru
    Processing:  12 Tuatapere 2180815
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tuatapere,nz
    Processing:  13 Butaritari 2110227
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=butaritari,ki
    Processing:  14 Karratha 6620339
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=karratha,au
    Processing:  15 Wanning 1791779
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=wanning,cn
    Processing:  16 Vanimo 2084442
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vanimo,pg
    Processing:  17 Ushuaia 3833367
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ushuaia,ar
    Processing:  18 Itigi 158904
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=itigi,tz
    Processing:  19 Alofi 4036284
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=alofi,nu
    Processing:  20 East London 1006984
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=east%20london,za
    Processing:  21 Gigmoto 1712961
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=gigmoto,ph
    Processing:  22 Brae 2654970
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=brae,gb
    Processing:  23 Kutum 371745
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kutum,sd
    Processing:  24 Provideniya 4031574
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=provideniya,ru
    Processing:  25 Vostok 2013279
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vostok,ru
    Processing:  26 Ahipara 2194098
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ahipara,nz
    Processing:  27 Bluff 2206939
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bluff,nz
    Processing:  28 Pskov 504341
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pskov,ru
    Processing:  29 Albany 2077963
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=albany,au
    Processing:  30 Salalah 286621
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=salalah,om
    Processing:  31 Vao 2137773
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vao,nc
    Processing:  32 Praia da Vitoria 3372760
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=praia%20da%20vitoria,pt
    Processing:  33 Belize 3582678
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=belize,bz
    Processing:  34 Saint-Philippe 935215
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=saint-philippe,re
    Processing:  35 Severo-Kurilsk 2121385
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=severo-kurilsk,ru
    Processing:  36 Sungaipenuh 1625929
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sungaipenuh,id
    Processing:  37 Tuktoyaktuk 6170031
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tuktoyaktuk,ca
    Processing:  38 Qaqortoq 3420846
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=qaqortoq,gl
    Processing:  39 Punta Arenas 3874787
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=punta%20arenas,cl
    Processing:  40 Esperance 2071860
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=esperance,au
    Processing:  41 Batagay 2027044
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=batagay,ru
    Processing:  42 Belfast 2655984
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=belfast,gb
    Processing:  43 Menongue 3347353
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=menongue,ao
    Processing:  44 New Norfolk 2155415
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=new%20norfolk,au
    Processing:  45 Saint-Augustin 6138501
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=saint-augustin,ca
    Processing:  46 Seymchan 2121373
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=seymchan,ru
    Processing:  47 Puerto Ayora 3652764
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=puerto%20ayora,ec
    Processing:  48 Atuona 4020109
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=atuona,pf
    Processing:  49 Mount Gambier 2156643
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mount%20gambier,au
    Processing:  50 Kodiak 4407665
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kodiak,us
    Processing:  51 Yellowknife 6185377
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yellowknife,ca
    Processing:  52 Ugoofaaru 1337619
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ugoofaaru,mv
    Processing:  53 Skjervoy 777682
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=skjervoy,no
    Processing:  54 Axim 2303611
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=axim,gh
    Processing:  55 Cabo San Lucas 3985710
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cabo%20san%20lucas,mx
    Processing:  56 Sorong 1626542
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sorong,id
    Processing:  57 Narsaq 3421719
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=narsaq,gl
    Processing:  58 Bull Savanna 3491161
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bull%20savanna,jm
    Processing:  59 Qaanaaq 3831208
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=qaanaaq,gl
    Processing:  60 Vila Velha 6320062
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vila%20velha,br
    Processing:  61 Baie-Comeau 5889745
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=baie-comeau,ca
    Processing:  62 Ilulissat 3423146
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ilulissat,gl
    Processing:  63 Ginir 336454
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ginir,et
    Processing:  64 Zemio 235826
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zemio,cf
    Processing:  65 Port Elizabeth 964420
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port%20elizabeth,za
    Processing:  66 Rock Sound 3571592
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rock%20sound,bs
    Processing:  67 Mar del Plata 3863379
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mar%20del%20plata,ar
    Processing:  68 Bathsheba 3374083
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bathsheba,bb
    Processing:  69 Iqaluit 5983720
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=iqaluit,ca
    Processing:  70 Tiksi 2015306
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tiksi,ru
    Processing:  71 Jijiga 333795
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=jijiga,et
    Processing:  72 Ishigaki 1861416
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ishigaki,jp
    Processing:  73 Shellbrook 6145951
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=shellbrook,ca
    Processing:  74 Avarua 4035715
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=avarua,ck
    Processing:  75 Hermanus 3366880
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hermanus,za
    Processing:  76 Calabar 2346229
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=calabar,ng
    Processing:  77 Bredasdorp 1015776
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bredasdorp,za
    Processing:  78 Hobart 2163355
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hobart,au
    Processing:  79 Cidreira 3466165
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cidreira,br
    Processing:  80 Riyadh 108410
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=riyadh,sa
    Processing:  81 Cape Town 3369157
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cape%20town,za
    Processing:  82 Clyde River 5924351
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=clyde%20river,ca
    Processing:  83 Portland 2152668
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=portland,au
    Processing:  84 Carnarvon 2074865
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=carnarvon,au
    Processing:  85 Souillac 933995
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=souillac,mu
    Processing:  86 Taoudenni 2450173
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=taoudenni,ml
    Processing:  87 Cermik 318766
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cermik,tr
    Processing:  88 Marsa Matruh 352733
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=marsa%20matruh,eg
    Processing:  89 Richards Bay 962367
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=richards%20bay,za
    Processing:  90 Itarema 3393692
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=itarema,br
    Processing:  91 Barrow 4252975
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=barrow,us
    Processing:  92 Yoichi 2129218
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yoichi,jp
    Processing:  93 Satipo 3928924
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=satipo,pe
    Processing:  94 Bedele 342567
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bedele,et
    Processing:  95 Caravelas 3466980
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=caravelas,br
    Processing:  96 Kayan 1319533
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kayan,mm
    Processing:  97 Cockburn Town 3576994
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cockburn%20town,tc
    Processing:  98 Zyryanovsk 1516438
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zyryanovsk,kz
    Processing:  99 Sioux Lookout 6148373
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sioux%20lookout,ca
    Processing:  100 Palmas 3474574
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=palmas,br
    Processing:  101 Sao Filipe 3374210
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sao%20filipe,cv
    Processing:  102 Scottsbluff 5699404
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=scottsbluff,us
    Processing:  103 Mildura 2157698
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mildura,au
    Processing:  104 Ponta do Sol 3374346
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ponta%20do%20sol,cv
    Processing:  105 Morehead 2090495
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=morehead,pg
    Processing:  106 Namatanai 2090021
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=namatanai,pg
    Processing:  107 Kyrylivka 696280
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kyrylivka,ua
    Processing:  108 Hervey Bay 2146219
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hervey%20bay,au
    Processing:  109 Hilo 5855927
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hilo,us
    Processing:  110 Ormara 1168700
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ormara,pk
    Processing:  111 Faanui 4034551
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=faanui,pf
    Processing:  112 Puerto Baquerizo Moreno 3652758
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=puerto%20baquerizo%20moreno,ec
    Processing:  113 Arraial do Cabo 3471451
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=arraial%20do%20cabo,br
    Processing:  114 Saskylakh 2017155
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=saskylakh,ru
    Processing:  115 Port Alfred 964432
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port%20alfred,za
    Processing:  116 Lere 2332079
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lere,ng
    Processing:  117 Longyearbyen 2729907
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=longyearbyen,sj
    Processing:  118 Presidencia Roque Saenz Pena 3840300
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=presidencia%20roque%20saenz%20pena,ar
    Processing:  119 Norman Wells 6089245
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=norman%20wells,ca
    Processing:  120 Egvekinot 4031742
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=egvekinot,ru
    Processing:  121 Myitkyina 1307741
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=myitkyina,mm
    Processing:  122 Torbay 6167817
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=torbay,ca
    Processing:  123 Kaitangata 2208248
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kaitangata,nz
    Processing:  124 Burgeo 5911440
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=burgeo,ca
    Processing:  125 Grand Gaube 934479
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=grand%20gaube,mu
    Processing:  126 Gazanjyk 161974
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=gazanjyk,tm
    Processing:  127 Ribeira Grande 3372707
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ribeira%20grande,pt
    Processing:  128 Rio Gallegos 3838859
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rio%20gallegos,ar
    Processing:  129 North Platte 5697939
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=north%20platte,us
    Processing:  130 Ponta Delgada 3372783
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ponta%20delgada,pt
    Processing:  131 Manokwari 1636308
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=manokwari,id
    Processing:  132 Grindavik 3416888
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=grindavik,is
    Processing:  133 Amazar 2027806
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=amazar,ru
    Processing:  134 Yelizovo 2119538
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yelizovo,ru
    Processing:  135 Port Lincoln 2063036
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port%20lincoln,au
    Processing:  136 San Patricio 3985168
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=san%20patricio,mx
    Processing:  137 Mahebourg 934322
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mahebourg,mu
    Processing:  138 Ostrovnoy 556268
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ostrovnoy,ru
    Processing:  139 Hithadhoo 1282256
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hithadhoo,mv
    Processing:  140 Fairbanks 5861897
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=fairbanks,us
    Processing:  141 Alice Springs 2077895
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=alice%20springs,au
    Processing:  142 Boa Vista 3664980
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=boa%20vista,br
    Processing:  143 Florida 3558771
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=florida,cu
    Processing:  144 Aklavik 5882953
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=aklavik,ca
    Processing:  145 Chuy 3443061
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=chuy,uy
    Processing:  146 Malchevskaya 526558
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=malchevskaya,ru
    Processing:  147 Yibin 1786770
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yibin,cn
    Processing:  148 Klenovyy 705673
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=klenovyy,ua
    Processing:  149 Kungurtug 1501377
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kungurtug,ru
    Processing:  150 Aracuai 3471846
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=aracuai,br
    Processing:  151 Megion 1499053
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=megion,ru
    Processing:  152 Pak Phanang 1608033
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pak%20phanang,th
    Processing:  153 Azul 3436199
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=azul,ar
    Processing:  154 Kindu 212902
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kindu,cd
    Processing:  155 Sunland Park 5493403
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sunland%20park,us
    Processing:  156 Jumla 1283285
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=jumla,np
    Processing:  157 Sambava 1056899
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sambava,mg
    Processing:  158 Lompoc 5367788
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lompoc,us
    Processing:  159 Sinnamary 3380290
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sinnamary,gf
    Processing:  160 Chokurdakh 2126123
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=chokurdakh,ru
    Processing:  161 Poum 2138555
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=poum,nc
    Processing:  162 Puri 1259184
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=puri,in
    Processing:  163 Kondinskoye 1502697
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kondinskoye,ru
    Processing:  164 Lebu 3883457
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lebu,cl
    Processing:  165 Washington 2634715
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=washington,gb
    Processing:  166 Fortuna 5563839
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=fortuna,us
    Processing:  167 Henties Bay 3356832
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=henties%20bay,na
    Processing:  168 Vila do Maio 3374120
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vila%20do%20maio,cv
    Processing:  169 Saint George 3573061
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=saint%20george,bm
    Processing:  170 Lodwar 189280
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lodwar,ke
    Processing:  171 Dikson 1507390
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dikson,ru
    Processing:  172 Raudeberg 3146487
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=raudeberg,no
    Processing:  173 Kyra 2021041
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kyra,ru
    Processing:  174 Cherskiy 2126199
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cherskiy,ru
    Processing:  175 Kavieng 2094342
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kavieng,pg
    Processing:  176 Pevek 2122090
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pevek,ru
    Processing:  177 Bilibino 2126682
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bilibino,ru
    Processing:  178 Abu Dhabi 292968
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=abu%20dhabi,ae
    Processing:  179 Komatsu 1858910
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=komatsu,jp
    Processing:  180 Miyako 1848087
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=miyako,jp
    Processing:  181 Pangnirtung 6096551
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pangnirtung,ca
    Processing:  182 Najran 103630
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=najran,sa
    Processing:  183 Linkoping 2694762
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=linkoping,se
    Processing:  184 Rocha 3440777
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rocha,uy
    Processing:  185 Frankfurt 3220802
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=frankfurt,de
    Processing:  186 Habartov 3076076
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=habartov,cz
    Processing:  187 Isangel 2136825
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=isangel,vu
    Processing:  188 Bubaque 2374583
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bubaque,gw
    Processing:  189 Kahului 5847411
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kahului,us
    Processing:  190 Pemberton 6100799
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pemberton,ca
    Processing:  191 Spitsevka 489671
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=spitsevka,ru
    Processing:  192 Hofn 2630299
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hofn,is
    Processing:  193 Georgetown 2411397
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=georgetown,sh
    Processing:  194 Nuuk 3421319
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=nuuk,gl
    Processing:  195 Omsukchan 2122493
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=omsukchan,ru
    Processing:  196 Kaitong 2036338
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kaitong,cn
    Processing:  197 Leningradskiy 2123814
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=leningradskiy,ru
    Processing:  198 Nizhneudinsk 1497549
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=nizhneudinsk,ru
    Processing:  199 Sfantu Gheorghe 667306
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sfantu%20gheorghe,ro
    Processing:  200 Kikwit 2314705
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kikwit,cd
    Processing:  201 Labuan 1734240
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=labuan,my
    Processing:  202 Amapa 3401225
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=amapa,br
    Processing:  203 Bonavista 5905393
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bonavista,ca
    Processing:  204 Hennenman 996918
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hennenman,za
    Processing:  205 Bloomingdale 4885156
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bloomingdale,us
    Processing:  206 Magole 155334
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=magole,tz
    Processing:  207 Angoche 1052944
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=angoche,mz
    Processing:  208 Toyota 1849814
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=toyota,jp
    Processing:  209 Coihaique 3894426
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=coihaique,cl
    Processing:  210 Upernavik 3418910
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=upernavik,gl
    Processing:  211 Yerbogachen 2012956
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yerbogachen,ru
    Processing:  212 Union 1685755
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=union,ph
    Processing:  213 Bordusani 684203
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bordusani,ro
    Processing:  214 Lorengau 2092164
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lorengau,pg
    Processing:  215 Castro 3896218
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=castro,cl
    Processing:  216 Lagoa 2267254
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lagoa,pt
    Processing:  217 Ambon 1651531
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ambon,id
    Processing:  218 Westport 2206900
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=westport,nz
    Processing:  219 Roma 2151187
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=roma,au
    Processing:  220 Upata 3625710
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=upata,ve
    Processing:  221 Banjar 1650233
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=banjar,id
    Processing:  222 Rawson 3839307
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rawson,ar
    Processing:  223 Inuvik 5983607
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=inuvik,ca
    Processing:  224 Victoria 241131
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=victoria,sc
    Processing:  225 Sitka 4267710
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sitka,us
    Processing:  226 Waterford 5278003
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=waterford,us
    Processing:  227 Deputatskiy 2028164
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=deputatskiy,ru
    Processing:  228 Kathmandu 1283240
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kathmandu,np
    Processing:  229 Cooma 2170577
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cooma,au
    Processing:  230 Katsuura 1865309
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=katsuura,jp
    Processing:  231 Geraldton 2070998
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=geraldton,au
    Processing:  232 Nikolskoye 546105
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=nikolskoye,ru
    Processing:  233 Flinders 6255012
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=flinders,au
    Processing:  234 Tasiilaq 3424607
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tasiilaq,gl
    Processing:  235 Houston 5977783
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=houston,ca
    Processing:  236 Gazimurskiy Zavod 2024122
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=gazimurskiy%20zavod,ru
    Processing:  237 Hami 1529484
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hami,cn
    Processing:  238 Sao Desiderio 3449304
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sao%20desiderio,br
    Processing:  239 Seoul 1835848
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=seoul,kr
    Processing:  240 Walvis Bay 3359638
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=walvis%20bay,na
    Processing:  241 Kieta 2094027
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kieta,pg
    Processing:  242 Benguela 3351663
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=benguela,ao
    Processing:  243 Camacha 2270385
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=camacha,pt
    Processing:  244 North Myrtle Beach 4589446
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=north%20myrtle%20beach,us
    Processing:  245 Vanavara 2013727
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vanavara,ru
    Processing:  246 Constitucion 4011743
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=constitucion,mx
    Processing:  247 Cap Malheureux 934649
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cap%20malheureux,mu
    Processing:  248 Yulara 6355222
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yulara,au
    Processing:  249 Bambous Virieux 1106677
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bambous%20virieux,mu
    Processing:  250 Koroni 259265
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=koroni,gr
    Processing:  251 Kaduqli 373141
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kaduqli,sd
    Processing:  252 Kenora 5991056
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kenora,ca
    Processing:  253 Soe 1626703
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=soe,id
    Processing:  254 San Rafael del Sur 3616594
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=san%20rafael%20del%20sur,ni
    Processing:  255 Cochabamba 3919968
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cochabamba,bo
    Processing:  256 Donduseni 618382
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=donduseni,md
    Processing:  257 Turbat 1163054
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=turbat,pk
    Processing:  258 Surt 2210554
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=surt,ly
    Processing:  259 Kaeo 2189343
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kaeo,nz
    Processing:  260 Adrar 2508813
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=adrar,dz
    Processing:  261 Kavaratti 1267390
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kavaratti,in
    Processing:  262 Port Arthur 4720039
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port%20arthur,us
    Processing:  263 Dibulla 3685223
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dibulla,co
    Processing:  264 Suamico 5274887
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=suamico,us
    Processing:  265 Mumbwa 904422
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mumbwa,zm
    Processing:  266 Barao de Melgaco 3470871
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=barao%20de%20melgaco,br
    Processing:  267 Teya 1489656
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=teya,ru
    Processing:  268 Port Blair 1259385
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port%20blair,in
    Processing:  269 Pitimbu 3391889
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pitimbu,br
    Processing:  270 Palmer 5871146
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=palmer,us
    Processing:  271 El Reno 4535783
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=el%20reno,us
    Processing:  272 Save 2391893
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=save,bj
    Processing:  273 Prieska 964090
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=prieska,za
    Processing:  274 Byron Bay 2172880
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=byron%20bay,au
    Processing:  275 Veraval 1253237
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=veraval,in
    Processing:  276 Olinda 3456160
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=olinda,br
    Processing:  277 Boende 218680
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=boende,cd
    Processing:  278 Aksarka 1512019
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=aksarka,ru
    Processing:  279 Tambau 3447005
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tambau,br
    Processing:  280 Xuzhou 1787824
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=xuzhou,cn
    Processing:  281 Bemidji 5017822
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bemidji,us
    Processing:  282 Bethel 5880568
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bethel,us
    Processing:  283 Tres Picos 3530097
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tres%20picos,mx
    Processing:  284 Basco 1726449
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=basco,ph
    Processing:  285 Namibe 3347019
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=namibe,ao
    Processing:  286 Buchanan 2278158
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=buchanan,lr
    Processing:  287 Rawlins 5836068
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rawlins,us
    Processing:  288 Mirabad 1133310
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mirabad,af
    Processing:  289 Carutapera 3402648
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=carutapera,br
    Processing:  290 La Asuncion 3480908
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=la%20asuncion,ve
    Processing:  291 Murdochville 6943820
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=murdochville,ca
    Processing:  292 Solo 1685850
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=solo,ph
    Processing:  293 Luderitz 3355672
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=luderitz,na
    Processing:  294 Kamaishi 2112444
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kamaishi,jp
    Processing:  295 Vanderhoof 6173361
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vanderhoof,ca
    Processing:  296 Hamilton 3573197
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hamilton,bm
    Processing:  297 Boulder City 5500539
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=boulder%20city,us
    Processing:  298 Neiafu 4032420
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=neiafu,to
    Processing:  299 Touros 3386213
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=touros,br
    Processing:  300 Te Anau 2181625
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=te%20anau,nz
    Processing:  301 Haines Junction 5969025
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=haines%20junction,ca
    Processing:  302 Dawson Creek 5935804
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dawson%20creek,ca
    Processing:  303 Villa Rica 3926120
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=villa%20rica,pe
    Processing:  304 Lexington Park 4360592
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lexington%20park,us
    Processing:  305 Mehamn 778707
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mehamn,no
    Processing:  306 Lipno 3093268
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lipno,pl
    Processing:  307 Pisco 3932145
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pisco,pe
    Processing:  308 Dauriya 2025099
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dauriya,ru
    Processing:  309 Ponazyrevo 506696
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ponazyrevo,ru
    Processing:  310 Gamba 2400547
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=gamba,ga
    Processing:  311 Ola 2122574
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ola,ru
    Processing:  312 Mairana 3910901
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mairana,bo
    Processing:  313 Sarauli 1262995
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sarauli,in
    Processing:  314 Nishihara 1850144
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=nishihara,jp
    Processing:  315 Hasaki 2112802
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hasaki,jp
    Processing:  316 Great Yarmouth 2647984
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=great%20yarmouth,gb
    Processing:  317 Sangar 2017215
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sangar,ru
    Processing:  318 Abu Kamal 174448
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=abu%20kamal,sy
    Processing:  319 Mahibadhoo 1337605
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mahibadhoo,mv
    Processing:  320 Kachug 2023333
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kachug,ru
    Processing:  321 Orange Cove 5379533
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=orange%20cove,us
    Processing:  322 Port Hardy 6111862
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port%20hardy,ca
    Processing:  323 Telimele 2414926
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=telimele,gn
    Processing:  324 Limbe 2229411
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=limbe,cm
    Processing:  325 Dalvik 2632287
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dalvik,is
    Processing:  326 Omboue 2396853
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=omboue,ga
    Processing:  327 Rosario 3838583
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rosario,ar
    Processing:  328 Los Llanos de Aridane 2514651
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=los%20llanos%20de%20aridane,es
    Processing:  329 Anta 3947634
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=anta,pe
    Processing:  330 Doha 290030
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=doha,qa
    Processing:  331 Skibbereen 2961459
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=skibbereen,ie
    Processing:  332 Havelock 4470244
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=havelock,us
    Processing:  333 Nanfeng 1795013
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=nanfeng,cn
    Processing:  334 Hereford 2647074
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hereford,gb
    Processing:  335 Hrubieszow 770966
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hrubieszow,pl
    Processing:  336 Nacala 1035025
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=nacala,mz
    Processing:  337 Rovaniemi 638936
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rovaniemi,fi
    Processing:  338 Itaituba 3397967
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=itaituba,br
    Processing:  339 Sarangani 1687186
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sarangani,ph
    Processing:  340 Balkanabat 161616
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=balkanabat,tm
    Processing:  341 Tiznit 2527089
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tiznit,ma
    Processing:  342 Amahai 1651591
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=amahai,id
    Processing:  343 Tongliao 2034400
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tongliao,cn
    Processing:  344 Coalinga 5338196
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=coalinga,us
    Processing:  345 Kendari 1640344
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kendari,id
    Processing:  346 Shubarshi 608270
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=shubarshi,kz
    Processing:  347 Tecoanapa 3532499
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tecoanapa,mx
    Processing:  348 Balikpapan 1650527
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=balikpapan,id
    Processing:  349 Hambantota 1244926
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hambantota,lk
    Processing:  350 Inverness 6945991
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=inverness,ca
    Processing:  351 Bima 1648759
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bima,id
    Processing:  352 Sao Miguel do Araguaia 3448455
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sao%20miguel%20do%20araguaia,br
    Processing:  353 La Grande 5735537
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=la%20grande,us
    Processing:  354 Dembi Dolo 339448
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dembi%20dolo,et
    Processing:  355 Mayo 6068416
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mayo,ca
    Processing:  356 Yuzawa 2110460
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yuzawa,jp
    Processing:  357 Anadyr 2127202
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=anadyr,ru
    Processing:  358 Polunochnoye 1494482
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=polunochnoye,ru
    Processing:  359 Muroto 1856392
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=muroto,jp
    Processing:  360 Magadan 2123628
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=magadan,ru
    Processing:  361 Ahuimanu 5856516
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ahuimanu,us
    Processing:  362 Lavrentiya 4031637
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lavrentiya,ru
    Processing:  363 Cabedelo 3404558
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cabedelo,br
    Processing:  364 Dingle 2964782
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dingle,ie
    Processing:  365 Ziro 1252668
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ziro,in
    Processing:  366 Samarai 2132606
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=samarai,pg
    Processing:  367 Port-Cartier 6111696
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port-cartier,ca
    Processing:  368 Bodden Town 3580733
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bodden%20town,ky
    Processing:  369 Candolim 1274989
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=candolim,in
    Processing:  370 Zhaozhou 2033147
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zhaozhou,cn
    Processing:  371 Mana 3381041
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mana,gf
    Processing:  372 Puerto Penasco 3991347
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=puerto%20penasco,mx
    Processing:  373 Sijunjung 1627185
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sijunjung,id
    Processing:  374 Puerto Rondon 3671337
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=puerto%20rondon,co
    Processing:  375 Broome 2075720
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=broome,au
    Processing:  376 Ceres 3369129
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ceres,za
    Processing:  377 Lillooet 6945979
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lillooet,ca
    Processing:  378 Alagoinha 3408094
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=alagoinha,br
    Processing:  379 Fort Nelson 5955902
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=fort%20nelson,ca
    Processing:  380 Alot 1278964
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=alot,in
    Processing:  381 Changping 2038154
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=changping,cn
    Processing:  382 Worthington 5053460
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=worthington,us
    Processing:  383 Hurricane 5540831
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=hurricane,us
    Processing:  384 Praya 1630662
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=praya,id
    Processing:  385 Oshikango 3353996
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=oshikango,na
    Processing:  386 Remanso 3408064
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=remanso,br
    Processing:  387 Namtsy 2019488
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=namtsy,ru
    Processing:  388 Sept-Iles 6144312
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sept-iles,ca
    Processing:  389 Aldan 2027968
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=aldan,ru
    Processing:  390 Douglas 4191916
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=douglas,us
    Processing:  391 Ixtapa 4004293
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ixtapa,mx
    Processing:  392 Raybag 1258278
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=raybag,in
    Processing:  393 Jian 1806445
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=jian,cn
    Processing:  394 Eydhafushi 1337606
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=eydhafushi,mv
    Processing:  395 Sanary-sur-Mer 2976258
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sanary-sur-mer,fr
    Processing:  396 Ostersund 2685750
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ostersund,se
    Processing:  397 Zambrano 3665616
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zambrano,co
    Processing:  398 Saint-Francois 3578441
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=saint-francois,gp
    Processing:  399 Araouane 2460954
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=araouane,ml
    Processing:  400 Zhigalovo 2012532
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zhigalovo,ru
    Processing:  401 Boca do Acre 3664956
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=boca%20do%20acre,br
    Processing:  402 Berlevag 780687
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=berlevag,no
    Processing:  403 Balakovo 579492
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=balakovo,ru
    Processing:  404 Kununurra 2068110
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kununurra,au
    Processing:  405 Praia 3374333
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=praia,cv
    Processing:  406 Pailon 3909010
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=pailon,bo
    Processing:  407 Varhaug 3132644
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=varhaug,no
    Processing:  408 Ardakan 143073
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ardakan,ir
    Processing:  409 Llangefni 2644037
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=llangefni,gb
    Processing:  410 Kudahuvadhoo 1337607
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kudahuvadhoo,mv
    Processing:  411 Kruisfontein 986717
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kruisfontein,za
    Processing:  412 Lucea 3489657
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lucea,jm
    Processing:  413 Midland 5526337
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=midland,us
    Processing:  414 Gravdal 3147822
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=gravdal,no
    Processing:  415 Jacobabad 1176515
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=jacobabad,pk
    Processing:  416 Cururupu 3401148
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=cururupu,br
    Processing:  417 Guerrero Negro 4021858
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=guerrero%20negro,mx
    Processing:  418 Qasigiannguit 3420768
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=qasigiannguit,gl
    Processing:  419 La Romana 3500957
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=la%20romana,do
    Processing:  420 Bershet 576745
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bershet,ru
    Processing:  421 Labuhan 1641899
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=labuhan,id
    Processing:  422 Dingli 2563140
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=dingli,mt
    Processing:  423 Mogadishu 53654
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mogadishu,so
    Processing:  424 Ossora 2122389
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ossora,ru
    Processing:  425 Jequitinhonha 3459925
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=jequitinhonha,br
    Processing:  426 Lusambo 210379
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=lusambo,cd
    Processing:  427 Russell 2188874
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=russell,nz
    Processing:  428 Forrest City 4111382
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=forrest%20city,us
    Processing:  429 Koslan 544084
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=koslan,ru
    Processing:  430 Talnakh 1490256
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=talnakh,ru
    Processing:  431 Yopal 3665688
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yopal,co
    Processing:  432 Ercis 315530
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ercis,tr
    Processing:  433 Zhanaozen 607610
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zhanaozen,kz
    Processing:  434 Progreso 3515690
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=progreso,mx
    Processing:  435 Iralaya 3608828
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=iralaya,hn
    Processing:  436 Shush 114593
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=shush,ir
    Processing:  437 Balad 98112
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=balad,iq
    Processing:  438 Krasnoborsk 542423
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=krasnoborsk,ru
    Processing:  439 Quang Ngai 1568770
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=quang%20ngai,vn
    Processing:  440 Auki 2109701
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=auki,sb
    Processing:  441 Beringovskiy 2126710
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=beringovskiy,ru
    Processing:  442 Eureka 5563397
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=eureka,us
    Processing:  443 Wamba 204318
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=wamba,cd
    Processing:  444 Kanevskaya 553152
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kanevskaya,ru
    Processing:  445 Acari 3948613
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=acari,pe
    Processing:  446 Ganzhou 1810638
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ganzhou,cn
    Processing:  447 Sisimiut 3419842
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sisimiut,gl
    Processing:  448 Groningen 3384125
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=groningen,sr
    Processing:  449 Tarauaca 3661980
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tarauaca,br
    Processing:  450 Laramie 5830062
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=laramie,us
    Processing:  451 Berberati 2389086
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=berberati,cf
    Processing:  452 Miraflores 3674735
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=miraflores,co
    Processing:  453 Weligama 1223738
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=weligama,lk
    Processing:  454 Mujiayingzi 2035707
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mujiayingzi,cn
    Processing:  455 Sorland 3137469
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sorland,no
    Processing:  456 Rio Grande 3451138
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rio%20grande,br
    Processing:  457 Urukh 478601
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=urukh,ru
    Processing:  458 Kumluca 305681
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kumluca,tr
    Processing:  459 Oriximina 3393471
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=oriximina,br
    Processing:  460 Kpalime 2365560
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kpalime,tg
    Processing:  461 Sukumo 1851462
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=sukumo,jp
    Processing:  462 Mwense 902721
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mwense,zm
    Processing:  463 Suvorovskaya 485871
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=suvorovskaya,ru
    Processing:  464 Vestmannaeyjar 3412093
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=vestmannaeyjar,is
    Processing:  465 Mount Isa 2065594
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=mount%20isa,au
    Processing:  466 Tpig 481900
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=tpig,ru
    Processing:  467 Coquimbo 3893629
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=coquimbo,cl
    Processing:  468 Zalesovo 1485528
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=zalesovo,ru
    Processing:  469 Piskavica 3199779
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=piskavica,ba
    Processing:  470 Kargil 1267776
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kargil,in
    Processing:  471 Verkh-Usugli 2013459
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=verkh-usugli,ru
    Processing:  472 Port Macquarie 2152659
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=port%20macquarie,au
    Processing:  473 Kankon 1268022
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=kankon,in
    Processing:  474 Khandyga 2022773
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=khandyga,ru
    Processing:  475 Buraydah 107304
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=buraydah,sa
    Processing:  476 Montepuez 1037125
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=montepuez,mz
    Processing:  477 Oranjemund 3354071
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=oranjemund,na
    Processing:  478 Albacete 2522258
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=albacete,es
    Processing:  479 Choya 1507745
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=choya,ru
    Processing:  480 Senanga 898947
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=senanga,zm
    Processing:  481 Atbasar 1526038
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=atbasar,kz
    Processing:  482 Otjimbingwe 3353871
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=otjimbingwe,na
    Processing:  483 Rabo de Peixe 3372745
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=rabo%20de%20peixe,pt
    Processing:  484 Florianopolis 3463237
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=florianopolis,br
    Processing:  485 Aykhal 2027296
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=aykhal,ru
    Processing:  486 Verkhoyansk 2013465
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=verkhoyansk,ru
    Processing:  487 Coahuayana 3981460
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=coahuayana,mx
    Processing:  488 Puerto Madero 3520989
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=puerto%20madero,mx
    Processing:  489 Arandis 3358670
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=arandis,na
    Processing:  490 Yinchuan 1786657
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=yinchuan,cn
    Processing:  491 Bandarbeyla 64814
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bandarbeyla,so
    Processing:  492 Casa Nova 3451474
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=casa%20nova,br
    Processing:  493 Nanortalik 3421765
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=nanortalik,gl
    Processing:  494 Bavly 578638
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=bavly,ru
    Processing:  495 Luanda 2240449
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=luanda,ao
    Processing:  496 Ashland 4282757
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ashland,us
    Processing:  497 Verkhnyaya Toyma 474470
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=verkhnyaya%20toyma,ru
    Processing:  498 Inta 1505579
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=inta,ru
    Processing:  499 Batagay-Alyta 2027042
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=batagay-alyta,ru
    Processing:  500 Ampanihy 1078553
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=95b385f5c0a646975b9f460480b7401c&q=ampanihy,mg
    


```python
all.to_csv('cities.csv')
print(all.count())
all.head()
```

    City          500
    CityID        500
    Cloudiness    500
    Country       500
    Date          500
    Humidity      500
    Latitude      500
    Longtitude    500
    Max Temp      500
    Wind Speed    500
    dtype: int64
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>CityID</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Latitude</th>
      <th>Longtitude</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Zhanakorgan</td>
      <td>1517323</td>
      <td>92</td>
      <td>KZ</td>
      <td>1522430186</td>
      <td>58</td>
      <td>43.91</td>
      <td>67.25</td>
      <td>68.50</td>
      <td>9.75</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Busselton</td>
      <td>2075265</td>
      <td>24</td>
      <td>AU</td>
      <td>1522430187</td>
      <td>100</td>
      <td>-33.64</td>
      <td>115.35</td>
      <td>64.72</td>
      <td>21.72</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Vaini</td>
      <td>4032243</td>
      <td>90</td>
      <td>TO</td>
      <td>1522429200</td>
      <td>100</td>
      <td>-21.20</td>
      <td>-175.20</td>
      <td>71.60</td>
      <td>18.70</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Thompson</td>
      <td>6165406</td>
      <td>20</td>
      <td>CA</td>
      <td>1522429200</td>
      <td>41</td>
      <td>55.74</td>
      <td>-97.86</td>
      <td>1.40</td>
      <td>12.75</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Rikitea</td>
      <td>4030556</td>
      <td>0</td>
      <td>PF</td>
      <td>1522430188</td>
      <td>100</td>
      <td>-23.12</td>
      <td>-134.97</td>
      <td>79.57</td>
      <td>11.54</td>
    </tr>
  </tbody>
</table>
</div>




```python
print('LATITUDE vs MAX TEMPERATURE PLOT')
plt.scatter(all["Latitude"], all["Max Temp"], marker="o")
plt.title("City Latitude vs. Max Temperature (03/30/2018)")
plt.ylabel("Max Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)
plt.axvline(0, color='black',alpha=0.5)
plt.savefig("LATvsTEMP.png")
plt.show()
```

    LATITUDE vs MAX TEMPERATURE PLOT
    


![png](output_4_1.png)



```python
print('LATITUDE vs HUMIDITY PLOT')
plt.scatter(all["Latitude"], all["Humidity"], marker="o")
plt.title("City Latitude vs. Humidity (03/30/2018)")
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.grid(True)
plt.axvline(0, color='black',alpha=0.5)
plt.savefig("LATvsHUMID.png")
plt.show()
```

    LATITUDE vs HUMIDITY PLOT
    


![png](output_5_1.png)



```python
print('LATITUDE vs CLOUDINESS PLOT')
plt.scatter(all["Latitude"], all["Cloudiness"], marker="o")
plt.title("City Latitude vs. Cloudiness (03/30/2018)")
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)
plt.axvline(0, color='black',alpha=0.5)
plt.savefig("LATvsCLOUD.png")
plt.show()
```

    LATITUDE vs CLOUDINESS PLOT
    


![png](output_6_1.png)



```python
print('LATITUDE vs WIND SPEED PLOT')
plt.scatter(all["Latitude"], all["Wind Speed"], marker="o")
plt.title("City Latitude vs. Wind Speed (03/30/2018)")
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")
plt.grid(True)
plt.axvline(0, color='black',alpha=0.5)
plt.savefig("LATvsWIND.png")
plt.show()

```

    LATITUDE vs WIND SPEED PLOT
    


![png](output_7_1.png)

