Instead of setting up an infrastructure with InfluxDb, Panorama or others, the KISS way is: 

* Make sure you installed the SSH & Web Terminal Addon
* Configure SSH
* Copy home-assistant_v2.db to your local machine
* Export sqlite to CSV

#  Copy home-assistant_v2.db to your local machine

```
scp hass:config/home-assistant_v2.db .
```

# Export sqlite to CSV

```
sqlite3 -header -csv home-assistant_v2.db "select * from states" > states.csv
```

Of course, you can choose to only export the rows of your interest.

E.g. to only select the metrics of my Xiaomi Mijia Bluetooth Thermometer & Hygrometer:

```
sqlite3 -header -csv home-assistant_v2.db "select * from states where entity_id='sensor.ble_temperature_xiaomi_hygro_thermometer_living_room'" > states.csv
```

#  Do your analytics

After exporting your data you can do your analysis in R, Python, Excel,...

For example, an R ggplot line plot of the temperature

```
library(tidyverse)
library(readr)
library(ggplot2)

states <- read_csv("states.csv", na = "unknown")

states %>% 
  filter(entity_id == "sensor.ble_temperature_xiaomi_hygro_thermometer_living_room") %>%
  mutate(state = as.double(state)) %>%
  ggplot(aes(x = created, y = state)) +
  geom_line()
```
