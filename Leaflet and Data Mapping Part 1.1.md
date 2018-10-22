# Leaflet and Data Mapping Part 1
#javascript

## 使用Leaflet
要使用Leaflet至少要有以下檔案：
1. index.html
2. logic.js
3. config.js
4. style.css

### index.html
在html的head中，以下三個部分要先被定義：
1. Leaflet CSS & JS
2. d3 JavaScript
3. Our CSS 
```html=
	<!-- Leaflet CSS & JS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.4/dist/leaflet.css"
  integrity="sha512-puBpdR0798OZvTTbP4A8Ix/l+A4dHDD0DGqYW6RQ+9jxkRFclaxxQb/SJAWZfWAkuyeQUytO7+7N4QKrDh+drA=="
  crossorigin=""/>

  <script src="https://unpkg.com/leaflet@1.3.4/dist/leaflet.js"
  integrity="sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA=="
  crossorigin=""></script>

  <!-- d3 JavaScript -->
  <script src="https://d3js.org/d3.v4.min.js"></script>

  <!-- Our CSS -->
  <link rel="stylesheet" type="text/css" href="./css/style.css">
```

然後在body中定義
1. map tag
2. 載入config.js：API key (存有mapbox的token)
3. 載入logic.js

### style.css
```css=
/* remove default margin and padding from body */
body {
  padding: 0;
  margin: 0;
}

/* set map, body, and html to 100% of the screen size */
#map,
body,
html {
  height: 100%;
}
```

### config.js
儲存mapbox的token
```javascript=
const API_KEY = 'pk.eyJ1IjoiZXVmbWlrZSIsImEiOiJjam5jM3ltNDkxczBnM3FvZWVva3RkdjFiIn0.vLXDx-MUeMXiRGTjuK4fXg';
```

### logic.js
在`logic.js`檔案下建構地圖，大致上可以分為以下三個步驟：

1. 用`L.map`建立地圖結構，包含地圖中心位置（`center`）跟縮放大小（`zoom`）。
2. 用`L.tileLayer`建立地圖圖層，決定主題跟數量。在這一步會需要知道accessToken。
3. 建立地圖上的向量物件，舉例如下：
	* `L.marker`
	* `L.polyline`
	* `L.polygon`
	* `L.rectangle`
	* `L.circle`
	* `L.geojson`

基本結構：
```javascript=
//Create initial map with id "map", defined in the index.html
var myMap = L.map("map", {
  center: [39.50, -98.35],
  zoom: 4
});
//==================================================================

//Create a map and fill in the container
var lightmap = L.tileLayer("https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}", {
  attribution: "Map data &copy; <a href=\"https://www.openstreetmap.org/\">OpenStreetMap</a> contributors, <a href=\"https://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA</a>, Imagery © <a href=\"https://www.mapbox.com/\">Mapbox</a>",
  maxZoom: 18,
  id: "mapbox.light",
  accessToken: API_KEY
});

//Use the addTo method to add objects to our map
lightmap.addTo(myMap); 
```

---
## 關於GeoJSON
* [官方網站](http://geojson.org)
* [Google Maps API - 顯示 GeoJSON 資料](https://www.oxxostudio.tw/articles/201803/google-maps-14-geojson.html)
* [WebGIS中的向量資料-在Leaflet實作](**WebGIS中的向量資料-在Leaflet實作**)

GeoJSON的基本結構為Feature，定義所有的向量物件，然後最外層用一個FeatureCollection把所有的Feature包起來。
```javascript=
{
  "type": "FeatureCollection",  //包起所有結構的FeatureCollection
  "features": [
    {	//個別物件
      "type": "Feature",
      "properties": {
        "stroke": "#ff0000",
        "stroke-width": 10,
        "stroke-opacity": 0.5
      },
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [
            121.56351685523987,
            25.03585799721269
          ],
          [
            121.56548023223877,
            25.0358093932627
          ]
        ]
      }
    }
  ]
}
```

以本次作業的geojson為例，最外層長這樣：
![](https://i.imgur.com/TeKQC1N.png)
除了符合基本結構的type跟features，還有額外的metadata跟bbox。

打開feature，則會看到基本結構type、properties跟geometry。另外還多了id。geometry則帶了type跟coordinates。
![](https://i.imgur.com/AZ5oGX9.png)

在geometry下type的部分，除了Point，還可以有LineString跟Polygon。這部分請參閱[官方文件](https://tools.ietf.org/rfc/rfc7946.txt)第三章。總共有下列物件：
```
3.  GeoJSON Object  . . . . . . . . . . . . . . . . . . . . . . .   6
     3.1.  Geometry Object . . . . . . . . . . . . . . . . . . . . .   7
       3.1.1.  Position  . . . . . . . . . . . . . . . . . . . . . .   7
       3.1.2.  Point . . . . . . . . . . . . . . . . . . . . . . . .   8
       3.1.3.  MultiPoint  . . . . . . . . . . . . . . . . . . . . .   8
       3.1.4.  LineString  . . . . . . . . . . . . . . . . . . . . .   8
       3.1.5.  MultiLineString . . . . . . . . . . . . . . . . . . .   8
       3.1.6.  Polygon . . . . . . . . . . . . . . . . . . . . . . .   9
       3.1.7.  MultiPolygon  . . . . . . . . . . . . . . . . . . . .   9
       3.1.8.  GeometryCollection  . . . . . . . . . . . . . . . . .   9
       3.1.9.  Antimeridian Cutting  . . . . . . . . . . . . . . . .  10
       3.1.10. Uncertainty and Precision . . . . . . . . . . . . . .  11
```

如果要自己產生物件，可以用這個工具繪製[geojson.io](http://geojson.io/)

---
## 用Leaflet畫出GeoJSON的資料
整理自：
[WebGIS中的向量資料-在Leaflet實作](**WebGIS中的向量資料-在Leaflet實作**) <- 簡短清楚
[Using GeoJSON with Leaflet - Leaflet - a JavaScript library for interactive maps](https://leafletjs.com/examples/geojson/) <- Leaflet使用GeoJSON的完整介紹

在leaflet中，把向量圖檔放在地圖上，有三種做法：
1. marker
2. path
	* Polyline
	* Polygon
	* Circle
	* CircleMarker
	* Rectangle
3. geojson
頭兩種方法，基本上就是把向量的資料餵給Leaflet，然後給它物件的指令，讓它把圖形畫出來。相對於這兩種方法，geojson則是直接把整個GeoJSON的資料給Leaflet讓它畫。

之所以我們可以把GeoJSON檔案整個丟給Leaflet，是因為Feature或FeatureCollection本身已經定義好結構跟樣式（請參閱* [Google Maps API - 顯示 GeoJSON 資料](https://www.oxxostudio.tw/articles/201803/google-maps-14-geojson.html)）。因此`L.geoJSON(data)`會自動匯入定義好的向量資訊。

在本次作業中，我們是先從USGS的網站（[feed頁面](https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php))），獲取一段指向geojson格式的網址（https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson），而非geojson檔案本身。因此需要先透過`d3.json()`這個功能擷取下json格式，存成變數，在交由`L.geojson()`畫圖。

最基本的結構長這樣：
```javascript=
// 產生一個url的變數
var url = 'https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson';

// 先用d3.json擷取url內json的資料，再pass給L.geojson
d3.json(url, function(data){
  var myLayer = L.geoJSON(data); //直接就可以產生圖層
  myLayer.addTo(myMap); //加進地圖裡就可以畫出了
  console.log(data); //測試用，可以看到data的結構
});
```

圖畫出來長這樣：
![](https://i.imgur.com/gDvdedE.jpg)


---
## 根據Data更動GeoJSON的顏色跟大小

### 第一步：先把point改成circle
接下來我們需要更動marker的樣式跟顏色，並加上legend。如果我們回去看GeoJSON的原始資料，會發現每一筆地震資料，`type`都是`Point`。但由於我們要根據地震震度大小（magnitude）來畫出相對應大小及顏色的圓圈，因此我們會改變一個geojson的argument叫做`**pointToLayer**`（在javascript下叫做option），把point重新用`L.circle`畫成circle。

要注意，使用`pointToLayer`的方法並不直觀（可參照[文件](https://leafletjs.com/reference-1.3.4.html#geojson)）。`pointToLayer`本身需要看到一串從geojson抓出來的資料，以及向量檔的風格，因此建立的方法使用一個nested function。

```javascript
/*A Function defining how GeoJSON points spawn Leaflet layers. It is internally called when data is added, passing the GeoJSON point feature and its ~LatLng~. The default is to spawn a default ~Marker~:*/

function(geoJsonPoint, latlng) {
    return L.marker(latlng);
}
```

然後，把這個function塞回去選項下，因此在我們的程式裡看起來會是這樣（注意，`pointToLayer`是`L.geoJSON`的一個選項而已，而且我們抓出`feature`跟`latlng`，但只用`latlng`）。：
```javascript=
d3.json(url, function(data){
  var myLayer = L.geoJSON(data, {
    pointToLayer: function (feature, latlng) {
      return L.circle(latlng, geojsonCircleOptions); //把latlng丟回去給L.Circle畫圖
    }
  });
  myLayer.addTo(myMap);
  console.log(data);
});
```

在這裏`geojsonCircleOptions`是我隨便定義的：
```javascript=
var geojsonCircleOptions = {
  radius: 8,
  fillColor: "#ff7800",
  color: "#000",
  weight: 0.5,
  opacity: 1,
  fillOpacity: 0.8
};
```

圖看起來像這樣：
![](https://i.imgur.com/NIvJuDO.png)

### 第二步：根據magnitude更動circle的大小
我們可以回過頭去看原始資料，或是在USGS的[網頁 GeoJSON Summary Format](https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php)上找到，`properties`下的`mag`就是我們要找的magnitude。

這時我們就要把`geojsonCircleOptions`下的radius，改成直接從`feature`拉出來的`mag`變數。但為了讓每個circle的大小會因為`mag`而改變，這裏得做點小更動。我們得把`geojsonCircleOptions`放在`pointToLayer`的function下，如此一來，我們才能利用從`L.geoJSON `抓出來的`feature`。

結果如下：
```javascript=
//Create function for add earthquake bubbles

//load data
var url = 'https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson';


d3.json(url, function(data){
  var myLayer = L.geoJSON(data, {
    pointToLayer: function(feature, latlng) {
      
		//Create marker options
      var geojsonCircleOptions = {
        radius: feature.properties.mag*5000,
        fillColor: "#ff7800",
        color: "#000",
        weight: 0.5,
        opacity: 1,
        fillOpacity: 0.8
      };      
      
      return L.circle(latlng, geojsonCircleOptions);
    }
  });
  myLayer.addTo(myMap);
  console.log(data);
});
```

在`radius: feature.properties.mag*5000` 這項，我們可以看到我把變數乘上`5000`，原因是一開始畫出來的圖circle都很小，回過頭去查`L.circle`的文件（[Documentation - Leaflet - a JavaScript library for interactive maps](https://leafletjs.com/reference-1.3.4.html#circle)）才發現，radius的單位是「公尺」。而我們的`mag`大多小於`10`，因此需要放大後才看得到。


作圖如下：
![](https://i.imgur.com/Ub1xFU9.png)


### 第三步：根據magnitude更動circle的顏色
這個部分參考至[Interactive Choropleth Map - Leaflet - a JavaScript library for interactive maps](https://leafletjs.com/examples/choropleth/)

首先，我們要先設定好顏色，顏色跟十六進位碼（HEX）可以從[colorbrewer](http://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3))挑選。
1. 先在上方的Number of data classes選擇顏色數目：這裡我們選`6`。
2. 選擇想使用的color scheme
3. 複製右下角的HEX code

然後，我們先寫一個function讓我們可以根據`mag`來選擇顏色。
```javascript
function getColor(d){
  return d > 5 ? '#bd0026' :
        d > 4  ? '#f03b20' :
        d > 3  ? '#fd8d3c' :
        d > 2  ? '#feb24c' :
        d > 1  ? '#fed976' :
                  '#ffffb2';
};
```
（若對於`?`使用不熟悉請參照文末）

接下來把`fillColor`改成如下：
```javascript
fillColor: getColor(feature.properties.mag),
```

這樣就可以根據`mag`回傳的數值來變更顏色，原始碼如下：
```javascript=
//Create function for add earthquake bubbles

//load data
var url = 'https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson';

function getColor(d){
  return d > 5 ? '#bd0026' :
        d > 4  ? '#f03b20' :
        d > 3  ? '#fd8d3c' :
        d > 2  ? '#feb24c' :
        d > 1  ? '#fed976' :
                  '#ffffb2';
};

d3.json(url, function(data){
  var myLayer = L.geoJSON(data, {
    pointToLayer: function(feature, latlng) {
      
      //Create marker options
      var geojsonCircleOptions = {
        radius: feature.properties.mag*7000,
        fillColor: getColor(feature.properties.mag),
        color: "#000",
        weight: 0.5,
        opacity: 1,
        fillOpacity: 0.8
      };      
      
      return L.circle(latlng, geojsonCircleOptions);
    }
  });
  myLayer.addTo(myMap);
  console.log(data);
});
```
注意：我在這邊改成放大7000倍

作圖如下：
![](https://i.imgur.com/gzMogCz.png)



### 第四步：建立Legend
這個部分也是參考至[Interactive Choropleth Map - Leaflet - a JavaScript library for interactive maps](https://leafletjs.com/examples/choropleth/)，最下面的**Custom Legend Control**。但因為貼上去稍微改了以下後就可以執行，因此沒有特別研究細節。

步驟如下：
1. 用`L.control`產生了一個`legend`的物件。`L.control`的[文件](https://leafletjs.com/reference-1.3.4.html#control)
2. 寫一個function，直接用`object.onAdd`塞一段html code進到`legend`物件中。為此，最後`return`的code是一段html code。

```javascript=
// 先產生一個legend物件，定義在右下角
var legend = L.control({position: 'bottomright'});

//用一個臨時function把html用onAdd的功能加進去legend裡
legend.onAdd = function (myMap) {

	//用L.DomUtil來產生一個DOM的節點，第一個變數是tag的名稱，第二個變數是class
    var div = L.DomUtil.create('div', 'info legend'),
	//產生區間
    grades = [0, 1, 2, 3, 4, 5], 
    labels = []; //雖然沒用到但還是要留著不知道為什麼

    // 對每個區間都產生一個顏色跟解說文字
    for (var i = 0; i < grades.length; i++) {
        div.innerHTML += //用+=來延長這段html code，不用擔心分行，因為有<br>會自己搞定
            '<i style="background:' + getColor(grades[i] + 1) + '"></i> ' +
            grades[i] + (grades[i + 1] ? '&ndash;' + grades[i + 1] + '<br>' : '+');
    }

    return div; //重要，回傳的就是html code
};

legend.addTo(myMap); //最後把legend這個物件家在地圖上
```

最後，因為這裡的html code只有顧到，如果只使用原始的css看起來會像這樣：
![](https://i.imgur.com/v6ryM4g.png)


為了讓legend可以被正確顯示，必須更新css檔來定義legend的範圍。

```css=
//==========================================================
//這邊是產生地圖時就應該使用的css
/* remove default margin and padding from body */
body {
  padding: 0;
  margin: 0;
}

/* set map, body, and html to 100% of the screen size */
#map,
body,
html {
  height: 100%;
}

//==========================================================
// 這邊是新增的legend
// 定義 legend要長多大，要不要外框
.legend {
  line-height: 18px;
  color: #555;
  background-color: #FFFFFFBF; //改底部顏色，最後兩碼是透明度
  border-radius: 5px; //邊角圓圓的好看
  padding: 10px; //決定padding的大小
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2); //加影子美觀
}
.legend i {
  width: 18px;
  height: 18px;
  float: left;
  margin-right: 8px;
  opacity: 0.8; //透明度選擇跟原本的圖一樣選0.8，這樣顏色才有辦法互相比對
}

```

這樣就完成第一部分的作業了。

---
## Conditional Operators的簡化
在此對`?`這個語法稍作解釋：這是一個if-else的簡化版[可以參考這裡](https://stackoverflow.com/questions/2595392/what-does-the-question-mark-and-the-colon-ternary-operator-mean-in-objectiv)。基本上`?`前就是Ture-False判斷，`?`後就是if true要執行的code，`:`後是if false要執行的code。
```javascript=
//所以以下這段code
result = (a >= 0) ? 'positive' : 'negative or zero';
//同等於
if(a >= 0) {
 result = 'positive';
} else {
 result = 'negative or zero';
}
```

而以下的寫法就等於把一連串的if-else串起來，所以可以根據不同的數值來輸出顏色。
```javascript=
function getColor(d){
  return d > 5 ? '#bd0026' :
        d > 4  ? '#f03b20' :
        d > 3  ? '#fd8d3c' :
        d > 2  ? '#feb24c' :
        d > 1  ? '#fed976' :
                  '#ffffb2';
};
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbOTgzNzAxNzE2XX0=
-->