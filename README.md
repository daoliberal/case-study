# case-study


## müşteri tipine göre ortalama sürüş
SELECT 
usertype,
FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(CAST(AVG(tripduration) AS INT64))) AS avg_ride_duration

 FROM `eminent-facet-292219.bikeshare1.bikeshare` 
group by usertype
---
select * from `eminent-facet-292219.bikeshare1.bikeshare` limit 100
-----
## müşteri tipine göre popüler rotaları bulmayı amaçlayan sorgu

select from_station_name, to_station_name,usertype, count(*) as popularite FROM `eminent-facet-292219.bikeshare1.bikeshare`
group by from_station_name, to_station_name,usertype
having usertype = 'Customer'
order by popularite desc
 limit 10000

-------
## haftanın günlerinde müşteri tipine göre sürüş ortalamaları
SELECT 
    usertype,
    EXTRACT(DAYOFWEEK FROM start_time) AS day_of_week,
    FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(CAST(AVG(tripduration) AS INT64))) AS avg_ride_duration
FROM 
    `eminent-facet-292219.bikeshare1.bikeshare` 
GROUP BY 
    usertype, 
    day_of_week
ORDER BY 
    usertype,
    day_of_week;

----
## müşteri tipine göre günün en talep gören saatleri
SELECT 
    usertype,
    EXTRACT(HOUR FROM start_time) AS hour_of_day,
    COUNT(*) as sayi
FROM 
    `eminent-facet-292219.bikeshare1.bikeshare` 
where usertype= 'Customer'
GROUP BY 
    usertype, 
    hour_of_day
ORDER BY 
sayi desc

