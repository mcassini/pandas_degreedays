pandas\_degreedays (ToDo list)
==============================

cumsum by year, by month - see group-by breakdown ?

    from pandas_degreedays.provider import WeatherHistory
    w = WeatherHistory('OpenWeatherMap', cache=..., ....)
    df = w.get(place, start_date, stop_date)

see projet <https://github.com/scls19fr/openweathermap_requests> to fetch historical weather data

    pip install openweathermap_requests

    $ python openweathermap_requests.py --range 20120101:20141215 -lon ... -lat ...

Read Excel file

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt

    df = pd.read_excel("openweathermap_0.34189_46.5798114_20120101_20141215.xls", skiprows=[1])
    #df = df.set_index('dt')
    idx = df.index
    s_idx = pd.Series(idx, index=idx)
    diff_idx = s_idx-s_idx.shift(1)
    #diff_idx = (s_idx-s_idx.shift(1))[1:]
    s_sampling_period = diff_idx.value_counts()
    sampling_period = s_sampling_period.index[0] # most prevalent sampling period
    not_sampling_period = (diff_idx != sampling_period) # True / False
    not_sampling_period = df.align(not_sampling_period, axis=0)[1].fillna(True)
    df['diff_dt'] = diff_idx.fillna(pd.Timedelta(0))

see also data\_quality.py

def calculate\_dd(ts\_temp, method='pro', typ='heating', Tref=18.0, group='yearly'):  
pass

group parameter should also support lambda function (applied to date) see function yearly\_month so we could count degree days yearly but from october the 1st (instead of january the 1st) see callable(group)
