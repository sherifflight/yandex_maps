# Yii2 Yandex Maps Components #

* * *

## Components ##

- [`mirocow\yandexmaps\Api`](https://github.com/mirocow/yii2-yandex-maps#yandexmapsapi)
- [`mirocow\yandexmaps\Map`](https://github.com/mirocow/yii2-yandex-maps#yandexmapsmap)
- [`mirocow\yandexmaps\Canvas`](https://github.com/mirocow/yii2-yandex-maps#yandexmapscanvas)
- `mirocow\yandexmaps\JavaScript`
- `mirocow\yandexmaps\Placemark`
- `mirocow\yandexmaps\Polyline`
- TODO: [Geo XML](http://api.yandex.ru/maps/doc/jsapi/2.x/dg/concepts/geoxml.xml)
- TODO: [GeoObject](http://api.yandex.ru/maps/doc/jsapi/2.x-stable/ref/reference/GeoObject.xml)
- TODO: [Balloon](http://api.yandex.ru/maps/doc/jsapi/2.x-stable/ref/reference/Balloon.xml)
- TODO: [Hint](http://api.yandex.ru/maps/doc/jsapi/2.x-stable/ref/reference/Hint.xml)
- TODO: [Clusterer](http://api.yandex.ru/maps/doc/jsapi/2.x/ref/reference/Clusterer.xml)

### mirocow\yandexmaps\Api ###

Application components which register scripts.

__Usage__

Attach component to application (e.g. edit config/main.php):
```php
'components' => [
	'yandexMapsApi' => [
		'class' => 'mirocow\yandexmaps\Api',
	]
 ],
```

### mirocow\yandexmaps\Map ###

Map instance.

__Usage__

```php
    $map = new YandexMap('yandex_map', [
            'center' => [55.7372, 37.6066],
            'zoom' => 10,
            // Enable zoom with mouse scroll
            'behaviors' => array('default', 'scrollZoom'),
            'type' => "yandex#map",
        ], 
        [
            // Permit zoom only fro 9 to 11
            'minZoom' => 9,
            'maxZoom' => 11,
            'controls' => [
              "new ymaps.control.SmallZoomControl()",
              "new ymaps.control.TypeSelector(['yandex#map', 'yandex#satellite'])",  
            ],                    
        ]                
    );             
```

### mirocow\yandexmaps\Canvas ###

This is widget which render html tag for your map.

__Usage__

Simple add widget to view:
```php

use mirocow\yandexmaps as YandexMaps;

echo YandexCanvas::widget([
        'htmlOptions' => [
            'style' => 'height: 400px;',
        ],
        'map' => $map,
    ]);
```

### mirocow\yandexmaps\Clusterer ###

```js
    for (var i in map_point) {
    points[i] = new ymaps.GeoObject({
     geometry : {
      type: 'Point',
      coordinates : [map_point[i]['lat'],map_point[i]['lng']]
     },
     properties : {
      balloonContentBody : map_point[i]['body']
      // hintContent : 'подробнее'
     }
    },
    {
     iconImageHref: '/i/' + map_point[i]['spec']+'.png',
     iconImageSize: [29,29],
     balloonIconImageHref: '/i/' + map_point[i]['spec']+'.png',
     balloonIconImageSize: [29,29],
     hasBalloon: true
    });
   }

   var clusterer = new ymaps.Clusterer();
   clusterer.add(points);
   map.geoObjects.add(clusterer);
```