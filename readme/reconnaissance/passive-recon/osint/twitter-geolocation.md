---
icon: location-dot
---

# Twitter Geolocation

## Twitter Geolocation

### Filter Tweet by Geographical Metadata

```
# Search String
geocode:-23.555488,-46.600370,10km url:wa.me “Gravidez”
```

* **geocode** = geolocation
* **radius** = determine a radius based on the region
* **url** = determine possible URL’s with this limitation

### Other Options

```
    geocode:-23.555488,-46.600370,10km url:wa.me filter:media
    geocode:-23.555488,-46.600370,20km url:wa.me “Drogas”
    geocode:-23.555488,-46.600370,40km url:fb.me “Gravidez”
    geocode:-23.555488,-46.600370,50km (wa.me OR fb.me) “Hacked”
    geocode:-23.555488,-46.600370,50km (wa.me OR fb.me) “Fake news”
    geocode:-23.555488,-46.600370,50km url:wa.me until:2020–08–01
    geocode:-23.555488,-46.600370,50km filter:links
```





***

## REFERENCES

* [https://debugactiveprocess.medium.com/osint-tips-filtering-tweets-by-geographical-metadata-cfba10fc4c87](https://debugactiveprocess.medium.com/osint-tips-filtering-tweets-by-geographical-metadata-cfba10fc4c87)
