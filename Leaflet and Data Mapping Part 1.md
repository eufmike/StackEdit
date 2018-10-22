---


---

<h1 id="leaflet-and-data-mapping-part-1">Leaflet and Data Mapping Part 1</h1>
<p>#javascript</p>
<h2 id="使用leaflet">使用Leaflet</h2>
<p>要使用Leaflet至少要有以下檔案：</p>
<ol>
<li>index.html</li>
<li>logic.js</li>
<li>config.js</li>
<li>style.css</li>
</ol>
<h3 id="index.html">index.html</h3>
<p>在html的head中，以下三個部分要先被定義：</p>
<ol>
<li>Leaflet CSS &amp; JS</li>
<li>d3 JavaScript</li>
<li>Our CSS</li>
</ol>
<pre class=" language-html"><code class="prism = language-html">	<span class="token comment">&lt;!-- Leaflet CSS &amp; JS --&gt;</span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>link</span> <span class="token attr-name">rel</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>stylesheet<span class="token punctuation">"</span></span> <span class="token attr-name">href</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://unpkg.com/leaflet@1.3.4/dist/leaflet.css<span class="token punctuation">"</span></span>
  <span class="token attr-name">integrity</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>sha512-puBpdR0798OZvTTbP4A8Ix/l+A4dHDD0DGqYW6RQ+9jxkRFclaxxQb/SJAWZfWAkuyeQUytO7+7N4QKrDh+drA==<span class="token punctuation">"</span></span>
  <span class="token attr-name">crossorigin</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span><span class="token punctuation">/&gt;</span></span>

  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://unpkg.com/leaflet@1.3.4/dist/leaflet.js<span class="token punctuation">"</span></span>
  <span class="token attr-name">integrity</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA==<span class="token punctuation">"</span></span>
  <span class="token attr-name">crossorigin</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript"></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>

  <span class="token comment">&lt;!-- d3 JavaScript --&gt;</span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://d3js.org/d3.v4.min.js<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript"></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>

  <span class="token comment">&lt;!-- Our CSS --&gt;</span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>link</span> <span class="token attr-name">rel</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>stylesheet<span class="token punctuation">"</span></span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>text/css<span class="token punctuation">"</span></span> <span class="token attr-name">href</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>./css/style.css<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>然後在body中定義</p>
<ol>
<li>map tag</li>
<li>載入config.js：API key (存有mapbox的token)</li>
<li>載入logic.js</li>
</ol>
<h3 id="style.css">style.css</h3>
<pre class=" language-css"><code class="prism = language-css"><span class="token comment">/* remove default margin and padding from body */</span>
<span class="token selector">body </span><span class="token punctuation">{</span>
  <span class="token property">padding</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
  <span class="token property">margin</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">/* set map, body, and html to 100% of the screen size */</span>
<span class="token selector"><span class="token id">#map</span>,
body,
html </span><span class="token punctuation">{</span>
  <span class="token property">height</span><span class="token punctuation">:</span> <span class="token number">100%</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="config.js">config.js</h3>
<p>儲存mapbox的token</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token keyword">const</span> API_KEY <span class="token operator">=</span> <span class="token string">'pk.eyJ1IjoiZXVmbWlrZSIsImEiOiJjam5jM3ltNDkxczBnM3FvZWVva3RkdjFiIn0.vLXDx-MUeMXiRGTjuK4fXg'</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="logic.js">logic.js</h3>
<p>在<code>logic.js</code>檔案下建構地圖，大致上可以分為以下三個步驟：</p>
<ol>
<li>用<code>L.map</code>建立地圖結構，包含地圖中心位置（<code>center</code>）跟縮放大小（<code>zoom</code>）。</li>
<li>用<code>L.tileLayer</code>建立地圖圖層，決定主題跟數量。在這一步會需要知道accessToken。</li>
<li>建立地圖上的向量物件，舉例如下：
<ul>
<li><code>L.marker</code></li>
<li><code>L.polyline</code></li>
<li><code>L.polygon</code></li>
<li><code>L.rectangle</code></li>
<li><code>L.circle</code></li>
<li><code>L.geojson</code></li>
</ul>
</li>
</ol>
<p>基本結構：</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token comment">//Create initial map with id "map", defined in the index.html</span>
<span class="token keyword">var</span> myMap <span class="token operator">=</span> L<span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span><span class="token string">"map"</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
  center<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token number">39.50</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">98.35</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
  zoom<span class="token punctuation">:</span> <span class="token number">4</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">//==================================================================</span>

<span class="token comment">//Create a map and fill in the container</span>
<span class="token keyword">var</span> lightmap <span class="token operator">=</span> L<span class="token punctuation">.</span><span class="token function">tileLayer</span><span class="token punctuation">(</span><span class="token string">"https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}"</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
  attribution<span class="token punctuation">:</span> <span class="token string">"Map data &amp;copy; &lt;a href=\"https://www.openstreetmap.org/\"&gt;OpenStreetMap&lt;/a&gt; contributors, &lt;a href=\"https://creativecommons.org/licenses/by-sa/2.0/\"&gt;CC-BY-SA&lt;/a&gt;, Imagery © &lt;a href=\"https://www.mapbox.com/\"&gt;Mapbox&lt;/a&gt;"</span><span class="token punctuation">,</span>
  maxZoom<span class="token punctuation">:</span> <span class="token number">18</span><span class="token punctuation">,</span>
  id<span class="token punctuation">:</span> <span class="token string">"mapbox.light"</span><span class="token punctuation">,</span>
  accessToken<span class="token punctuation">:</span> API_KEY
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">//Use the addTo method to add objects to our map</span>
lightmap<span class="token punctuation">.</span><span class="token function">addTo</span><span class="token punctuation">(</span>myMap<span class="token punctuation">)</span><span class="token punctuation">;</span> 
</code></pre>
<hr>
<h2 id="關於geojson">關於GeoJSON</h2>
<ul>
<li><a href="http://geojson.org">官方網站</a></li>
<li><a href="https://www.oxxostudio.tw/articles/201803/google-maps-14-geojson.html">Google Maps API - 顯示 GeoJSON 資料</a></li>
<li><a href="**WebGIS%E4%B8%AD%E7%9A%84%E5%90%91%E9%87%8F%E8%B3%87%E6%96%99-%E5%9C%A8Leaflet%E5%AF%A6%E4%BD%9C**">WebGIS中的向量資料-在Leaflet實作</a></li>
</ul>
<p>GeoJSON的基本結構為Feature，定義所有的向量物件，然後最外層用一個FeatureCollection把所有的Feature包起來。</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token punctuation">{</span>
  <span class="token string">"type"</span><span class="token punctuation">:</span> <span class="token string">"FeatureCollection"</span><span class="token punctuation">,</span>  <span class="token comment">//包起所有結構的FeatureCollection</span>
  <span class="token string">"features"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>	<span class="token comment">//個別物件</span>
      <span class="token string">"type"</span><span class="token punctuation">:</span> <span class="token string">"Feature"</span><span class="token punctuation">,</span>
      <span class="token string">"properties"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token string">"stroke"</span><span class="token punctuation">:</span> <span class="token string">"#ff0000"</span><span class="token punctuation">,</span>
        <span class="token string">"stroke-width"</span><span class="token punctuation">:</span> <span class="token number">10</span><span class="token punctuation">,</span>
        <span class="token string">"stroke-opacity"</span><span class="token punctuation">:</span> <span class="token number">0.5</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token string">"geometry"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token string">"type"</span><span class="token punctuation">:</span> <span class="token string">"LineString"</span><span class="token punctuation">,</span>
        <span class="token string">"coordinates"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
          <span class="token punctuation">[</span>
            <span class="token number">121.56351685523987</span><span class="token punctuation">,</span>
            <span class="token number">25.03585799721269</span>
          <span class="token punctuation">]</span><span class="token punctuation">,</span>
          <span class="token punctuation">[</span>
            <span class="token number">121.56548023223877</span><span class="token punctuation">,</span>
            <span class="token number">25.0358093932627</span>
          <span class="token punctuation">]</span>
        <span class="token punctuation">]</span>
      <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<p>以本次作業的geojson為例，最外層長這樣：<br>
<img src="https://i.imgur.com/TeKQC1N.png" alt=""><br>
除了符合基本結構的type跟features，還有額外的metadata跟bbox。</p>
<p>打開feature，則會看到基本結構type、properties跟geometry。另外還多了id。geometry則帶了type跟coordinates。<br>
<img src="https://i.imgur.com/AZ5oGX9.png" alt=""></p>
<p>在geometry下type的部分，除了Point，還可以有LineString跟Polygon。這部分請參閱<a href="https://tools.ietf.org/rfc/rfc7946.txt">官方文件</a>第三章。總共有下列物件：</p>
<pre><code>3.  GeoJSON Object  . . . . . . . . . . . . . . . . . . . . . . .   6
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
</code></pre>
<p>如果要自己產生物件，可以用這個工具繪製<a href="http://geojson.io/">geojson.io</a></p>
<hr>
<h2 id="用leaflet畫出geojson的資料">用Leaflet畫出GeoJSON的資料</h2>
<p>整理自：<br>
<a href="**WebGIS%E4%B8%AD%E7%9A%84%E5%90%91%E9%87%8F%E8%B3%87%E6%96%99-%E5%9C%A8Leaflet%E5%AF%A6%E4%BD%9C**">WebGIS中的向量資料-在Leaflet實作</a> &lt;- 簡短清楚<br>
<a href="https://leafletjs.com/examples/geojson/">Using GeoJSON with Leaflet - Leaflet - a JavaScript library for interactive maps</a> &lt;- Leaflet使用GeoJSON的完整介紹</p>
<p>在leaflet中，把向量圖檔放在地圖上，有三種做法：</p>
<ol>
<li>marker</li>
<li>path
<ul>
<li>Polyline</li>
<li>Polygon</li>
<li>Circle</li>
<li>CircleMarker</li>
<li>Rectangle</li>
</ul>
</li>
<li>geojson<br>
頭兩種方法，基本上就是把向量的資料餵給Leaflet，然後給它物件的指令，讓它把圖形畫出來。相對於這兩種方法，geojson則是直接把整個GeoJSON的資料給Leaflet讓它畫。</li>
</ol>
<p>之所以我們可以把GeoJSON檔案整個丟給Leaflet，是因為Feature或FeatureCollection本身已經定義好結構跟樣式（請參閱* <a href="https://www.oxxostudio.tw/articles/201803/google-maps-14-geojson.html">Google Maps API - 顯示 GeoJSON 資料</a>）。因此<code>L.geoJSON(data)</code>會自動匯入定義好的向量資訊。</p>
<p>在本次作業中，我們是先從USGS的網站（<a href="https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php">feed頁面</a>)），獲取一段指向geojson格式的網址（<a href="https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson%EF%BC%89%EF%BC%8C%E8%80%8C%E9%9D%9Egeojson%E6%AA%94%E6%A1%88%E6%9C%AC%E8%BA%AB%E3%80%82%E5%9B%A0%E6%AD%A4%E9%9C%80%E8%A6%81%E5%85%88%E9%80%8F%E9%81%8E">https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson），而非geojson檔案本身。因此需要先透過</a><code>d3.json()</code>這個功能擷取下json格式，存成變數，在交由<code>L.geojson()</code>畫圖。</p>
<p>最基本的結構長這樣：</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token comment">// 產生一個url的變數</span>
<span class="token keyword">var</span> url <span class="token operator">=</span> <span class="token string">'https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson'</span><span class="token punctuation">;</span>

<span class="token comment">// 先用d3.json擷取url內json的資料，再pass給L.geojson</span>
d3<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> <span class="token keyword">function</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">{</span>
  <span class="token keyword">var</span> myLayer <span class="token operator">=</span> L<span class="token punctuation">.</span><span class="token function">geoJSON</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//直接就可以產生圖層</span>
  myLayer<span class="token punctuation">.</span><span class="token function">addTo</span><span class="token punctuation">(</span>myMap<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//加進地圖裡就可以畫出了</span>
  console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//測試用，可以看到data的結構</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>圖畫出來長這樣：<br>
<img src="https://i.imgur.com/gDvdedE.jpg" alt=""></p>
<hr>
<h2 id="根據data更動geojson的顏色跟大小">根據Data更動GeoJSON的顏色跟大小</h2>
<h3 id="第一步：先把point改成circle">第一步：先把point改成circle</h3>
<p>接下來我們需要更動marker的樣式跟顏色，並加上legend。如果我們回去看GeoJSON的原始資料，會發現每一筆地震資料，<code>type</code>都是<code>Point</code>。但由於我們要根據地震震度大小（magnitude）來畫出相對應大小及顏色的圓圈，因此我們會改變一個geojson的argument叫做<code>**pointToLayer**</code>（在javascript下叫做option），把point重新用<code>L.circle</code>畫成circle。</p>
<p>要注意，使用<code>pointToLayer</code>的方法並不直觀（可參照<a href="https://leafletjs.com/reference-1.3.4.html#geojson">文件</a>）。<code>pointToLayer</code>本身需要看到一串從geojson抓出來的資料，以及向量檔的風格，因此建立的方法使用一個nested function。</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token comment">/*A Function defining how GeoJSON points spawn Leaflet layers. It is internally called when data is added, passing the GeoJSON point feature and its ~LatLng~. The default is to spawn a default ~Marker~:*/</span>

<span class="token keyword">function</span><span class="token punctuation">(</span>geoJsonPoint<span class="token punctuation">,</span> latlng<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> L<span class="token punctuation">.</span><span class="token function">marker</span><span class="token punctuation">(</span>latlng<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>然後，把這個function塞回去選項下，因此在我們的程式裡看起來會是這樣（注意，<code>pointToLayer</code>是<code>L.geoJSON</code>的一個選項而已，而且我們抓出<code>feature</code>跟<code>latlng</code>，但只用<code>latlng</code>）。：</p>
<pre class=" language-javascript"><code class="prism = language-javascript">d3<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> <span class="token keyword">function</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">{</span>
  <span class="token keyword">var</span> myLayer <span class="token operator">=</span> L<span class="token punctuation">.</span><span class="token function">geoJSON</span><span class="token punctuation">(</span>data<span class="token punctuation">,</span> <span class="token punctuation">{</span>
    pointToLayer<span class="token punctuation">:</span> <span class="token keyword">function</span> <span class="token punctuation">(</span>feature<span class="token punctuation">,</span> latlng<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      <span class="token keyword">return</span> L<span class="token punctuation">.</span><span class="token function">circle</span><span class="token punctuation">(</span>latlng<span class="token punctuation">,</span> geojsonCircleOptions<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//把latlng丟回去給L.Circle畫圖</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  myLayer<span class="token punctuation">.</span><span class="token function">addTo</span><span class="token punctuation">(</span>myMap<span class="token punctuation">)</span><span class="token punctuation">;</span>
  console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>在這裏<code>geojsonCircleOptions</code>是我隨便定義的：</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token keyword">var</span> geojsonCircleOptions <span class="token operator">=</span> <span class="token punctuation">{</span>
  radius<span class="token punctuation">:</span> <span class="token number">8</span><span class="token punctuation">,</span>
  fillColor<span class="token punctuation">:</span> <span class="token string">"#ff7800"</span><span class="token punctuation">,</span>
  color<span class="token punctuation">:</span> <span class="token string">"#000"</span><span class="token punctuation">,</span>
  weight<span class="token punctuation">:</span> <span class="token number">0.5</span><span class="token punctuation">,</span>
  opacity<span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">,</span>
  fillOpacity<span class="token punctuation">:</span> <span class="token number">0.8</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<p>圖看起來像這樣：<br>
<img src="https://i.imgur.com/NIvJuDO.png" alt=""></p>
<h3 id="第二步：根據magnitude更動circle的大小">第二步：根據magnitude更動circle的大小</h3>
<p>我們可以回過頭去看原始資料，或是在USGS的<a href="https://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php">網頁 GeoJSON Summary Format</a>上找到，<code>properties</code>下的<code>mag</code>就是我們要找的magnitude。</p>
<p>這時我們就要把<code>geojsonCircleOptions</code>下的radius，改成直接從<code>feature</code>拉出來的<code>mag</code>變數。但為了讓每個circle的大小會因為<code>mag</code>而改變，這裏得做點小更動。我們得把<code>geojsonCircleOptions</code>放在<code>pointToLayer</code>的function下，如此一來，我們才能利用從<code>L.geoJSON</code>抓出來的<code>feature</code>。</p>
<p>結果如下：</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token comment">//Create function for add earthquake bubbles</span>

<span class="token comment">//load data</span>
<span class="token keyword">var</span> url <span class="token operator">=</span> <span class="token string">'https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson'</span><span class="token punctuation">;</span>


d3<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> <span class="token keyword">function</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">{</span>
  <span class="token keyword">var</span> myLayer <span class="token operator">=</span> L<span class="token punctuation">.</span><span class="token function">geoJSON</span><span class="token punctuation">(</span>data<span class="token punctuation">,</span> <span class="token punctuation">{</span>
    pointToLayer<span class="token punctuation">:</span> <span class="token keyword">function</span><span class="token punctuation">(</span>feature<span class="token punctuation">,</span> latlng<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      
		<span class="token comment">//Create marker options</span>
      <span class="token keyword">var</span> geojsonCircleOptions <span class="token operator">=</span> <span class="token punctuation">{</span>
        radius<span class="token punctuation">:</span> feature<span class="token punctuation">.</span>properties<span class="token punctuation">.</span>mag<span class="token operator">*</span><span class="token number">5000</span><span class="token punctuation">,</span>
        fillColor<span class="token punctuation">:</span> <span class="token string">"#ff7800"</span><span class="token punctuation">,</span>
        color<span class="token punctuation">:</span> <span class="token string">"#000"</span><span class="token punctuation">,</span>
        weight<span class="token punctuation">:</span> <span class="token number">0.5</span><span class="token punctuation">,</span>
        opacity<span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">,</span>
        fillOpacity<span class="token punctuation">:</span> <span class="token number">0.8</span>
      <span class="token punctuation">}</span><span class="token punctuation">;</span>      
      
      <span class="token keyword">return</span> L<span class="token punctuation">.</span><span class="token function">circle</span><span class="token punctuation">(</span>latlng<span class="token punctuation">,</span> geojsonCircleOptions<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  myLayer<span class="token punctuation">.</span><span class="token function">addTo</span><span class="token punctuation">(</span>myMap<span class="token punctuation">)</span><span class="token punctuation">;</span>
  console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>在<code>radius: feature.properties.mag*5000</code> 這項，我們可以看到我把變數乘上<code>5000</code>，原因是一開始畫出來的圖circle都很小，回過頭去查<code>L.circle</code>的文件（<a href="https://leafletjs.com/reference-1.3.4.html#circle">Documentation - Leaflet - a JavaScript library for interactive maps</a>）才發現，radius的單位是「公尺」。而我們的<code>mag</code>大多小於<code>10</code>，因此需要放大後才看得到。</p>
<p>作圖如下：<br>
<img src="https://i.imgur.com/Ub1xFU9.png" alt=""></p>
<h3 id="第三步：根據magnitude更動circle的顏色">第三步：根據magnitude更動circle的顏色</h3>
<p>這個部分參考至<a href="https://leafletjs.com/examples/choropleth/">Interactive Choropleth Map - Leaflet - a JavaScript library for interactive maps</a></p>
<p>首先，我們要先設定好顏色，顏色跟十六進位碼（HEX）可以從<a href="http://colorbrewer2.org/#type=sequential&amp;scheme=BuGn&amp;n=3">colorbrewer</a>)挑選。</p>
<ol>
<li>先在上方的Number of data classes選擇顏色數目：這裡我們選<code>6</code>。</li>
<li>選擇想使用的color scheme</li>
<li>複製右下角的HEX code</li>
</ol>
<p>然後，我們先寫一個function讓我們可以根據<code>mag</code>來選擇顏色。</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">function</span> <span class="token function">getColor</span><span class="token punctuation">(</span>d<span class="token punctuation">)</span><span class="token punctuation">{</span>
  <span class="token keyword">return</span> d <span class="token operator">&gt;</span> <span class="token number">5</span> <span class="token operator">?</span> <span class="token string">'#bd0026'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">4</span>  <span class="token operator">?</span> <span class="token string">'#f03b20'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">3</span>  <span class="token operator">?</span> <span class="token string">'#fd8d3c'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">2</span>  <span class="token operator">?</span> <span class="token string">'#feb24c'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">1</span>  <span class="token operator">?</span> <span class="token string">'#fed976'</span> <span class="token punctuation">:</span>
                  <span class="token string">'#ffffb2'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<p>（若對於<code>?</code>使用不熟悉請參照文末）</p>
<p>接下來把<code>fillColor</code>改成如下：</p>
<pre class=" language-javascript"><code class="prism  language-javascript">fillColor<span class="token punctuation">:</span> <span class="token function">getColor</span><span class="token punctuation">(</span>feature<span class="token punctuation">.</span>properties<span class="token punctuation">.</span>mag<span class="token punctuation">)</span><span class="token punctuation">,</span>
</code></pre>
<p>這樣就可以根據<code>mag</code>回傳的數值來變更顏色，原始碼如下：</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token comment">//Create function for add earthquake bubbles</span>

<span class="token comment">//load data</span>
<span class="token keyword">var</span> url <span class="token operator">=</span> <span class="token string">'https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson'</span><span class="token punctuation">;</span>

<span class="token keyword">function</span> <span class="token function">getColor</span><span class="token punctuation">(</span>d<span class="token punctuation">)</span><span class="token punctuation">{</span>
  <span class="token keyword">return</span> d <span class="token operator">&gt;</span> <span class="token number">5</span> <span class="token operator">?</span> <span class="token string">'#bd0026'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">4</span>  <span class="token operator">?</span> <span class="token string">'#f03b20'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">3</span>  <span class="token operator">?</span> <span class="token string">'#fd8d3c'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">2</span>  <span class="token operator">?</span> <span class="token string">'#feb24c'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">1</span>  <span class="token operator">?</span> <span class="token string">'#fed976'</span> <span class="token punctuation">:</span>
                  <span class="token string">'#ffffb2'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

d3<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> <span class="token keyword">function</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">{</span>
  <span class="token keyword">var</span> myLayer <span class="token operator">=</span> L<span class="token punctuation">.</span><span class="token function">geoJSON</span><span class="token punctuation">(</span>data<span class="token punctuation">,</span> <span class="token punctuation">{</span>
    pointToLayer<span class="token punctuation">:</span> <span class="token keyword">function</span><span class="token punctuation">(</span>feature<span class="token punctuation">,</span> latlng<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      
      <span class="token comment">//Create marker options</span>
      <span class="token keyword">var</span> geojsonCircleOptions <span class="token operator">=</span> <span class="token punctuation">{</span>
        radius<span class="token punctuation">:</span> feature<span class="token punctuation">.</span>properties<span class="token punctuation">.</span>mag<span class="token operator">*</span><span class="token number">7000</span><span class="token punctuation">,</span>
        fillColor<span class="token punctuation">:</span> <span class="token function">getColor</span><span class="token punctuation">(</span>feature<span class="token punctuation">.</span>properties<span class="token punctuation">.</span>mag<span class="token punctuation">)</span><span class="token punctuation">,</span>
        color<span class="token punctuation">:</span> <span class="token string">"#000"</span><span class="token punctuation">,</span>
        weight<span class="token punctuation">:</span> <span class="token number">0.5</span><span class="token punctuation">,</span>
        opacity<span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">,</span>
        fillOpacity<span class="token punctuation">:</span> <span class="token number">0.8</span>
      <span class="token punctuation">}</span><span class="token punctuation">;</span>      
      
      <span class="token keyword">return</span> L<span class="token punctuation">.</span><span class="token function">circle</span><span class="token punctuation">(</span>latlng<span class="token punctuation">,</span> geojsonCircleOptions<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  myLayer<span class="token punctuation">.</span><span class="token function">addTo</span><span class="token punctuation">(</span>myMap<span class="token punctuation">)</span><span class="token punctuation">;</span>
  console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>注意：我在這邊改成放大7000倍</p>
<p>作圖如下：<br>
<img src="https://i.imgur.com/gzMogCz.png" alt=""></p>
<h3 id="第四步：建立legend">第四步：建立Legend</h3>
<p>這個部分也是參考至<a href="https://leafletjs.com/examples/choropleth/">Interactive Choropleth Map - Leaflet - a JavaScript library for interactive maps</a>，最下面的<strong>Custom Legend Control</strong>。但因為貼上去稍微改了以下後就可以執行，因此沒有特別研究細節。</p>
<p>步驟如下：</p>
<ol>
<li>用<code>L.control</code>產生了一個<code>legend</code>的物件。<code>L.control</code>的<a href="https://leafletjs.com/reference-1.3.4.html#control">文件</a></li>
<li>寫一個function，直接用<code>object.onAdd</code>塞一段html code進到<code>legend</code>物件中。為此，最後<code>return</code>的code是一段html code。</li>
</ol>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token comment">// 先產生一個legend物件，定義在右下角</span>
<span class="token keyword">var</span> legend <span class="token operator">=</span> L<span class="token punctuation">.</span><span class="token function">control</span><span class="token punctuation">(</span><span class="token punctuation">{</span>position<span class="token punctuation">:</span> <span class="token string">'bottomright'</span><span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">//用一個臨時function把html用onAdd的功能加進去legend裡</span>
legend<span class="token punctuation">.</span><span class="token function-variable function">onAdd</span> <span class="token operator">=</span> <span class="token keyword">function</span> <span class="token punctuation">(</span>myMap<span class="token punctuation">)</span> <span class="token punctuation">{</span>

	<span class="token comment">//用L.DomUtil來產生一個DOM的節點，第一個變數是tag的名稱，第二個變數是class</span>
    <span class="token keyword">var</span> div <span class="token operator">=</span> L<span class="token punctuation">.</span>DomUtil<span class="token punctuation">.</span><span class="token function">create</span><span class="token punctuation">(</span><span class="token string">'div'</span><span class="token punctuation">,</span> <span class="token string">'info legend'</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
	<span class="token comment">//產生區間</span>
    grades <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">,</span> <span class="token number">5</span><span class="token punctuation">]</span><span class="token punctuation">,</span> 
    labels <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span> <span class="token comment">//雖然沒用到但還是要留著不知道為什麼</span>

    <span class="token comment">// 對每個區間都產生一個顏色跟解說文字</span>
    <span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">var</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> grades<span class="token punctuation">.</span>length<span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        div<span class="token punctuation">.</span>innerHTML <span class="token operator">+=</span> <span class="token comment">//用+=來延長這段html code，不用擔心分行，因為有&lt;br&gt;會自己搞定</span>
            <span class="token string">'&lt;i style="background:'</span> <span class="token operator">+</span> <span class="token function">getColor</span><span class="token punctuation">(</span>grades<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token string">'"&gt;&lt;/i&gt; '</span> <span class="token operator">+</span>
            grades<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">+</span> <span class="token punctuation">(</span>grades<span class="token punctuation">[</span>i <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">?</span> <span class="token string">'&amp;ndash;'</span> <span class="token operator">+</span> grades<span class="token punctuation">[</span>i <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">+</span> <span class="token string">'&lt;br&gt;'</span> <span class="token punctuation">:</span> <span class="token string">'+'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">return</span> div<span class="token punctuation">;</span> <span class="token comment">//重要，回傳的就是html code</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

legend<span class="token punctuation">.</span><span class="token function">addTo</span><span class="token punctuation">(</span>myMap<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//最後把legend這個物件家在地圖上</span>
</code></pre>
<p>最後，因為這裡的html code只有顧到，如果只使用原始的css看起來會像這樣：<br>
<img src="https://i.imgur.com/v6ryM4g.png" alt=""></p>
<p>為了讓legend可以被正確顯示，必須更新css檔來定義legend的範圍。</p>
<pre class=" language-css"><code class="prism = language-css">//==========================================================
//這邊是產生地圖時就應該使用的css
<span class="token comment">/* remove default margin and padding from body */</span>
<span class="token selector">body </span><span class="token punctuation">{</span>
  <span class="token property">padding</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
  <span class="token property">margin</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">/* set map, body, and html to 100% of the screen size */</span>
<span class="token selector"><span class="token id">#map</span>,
body,
html </span><span class="token punctuation">{</span>
  <span class="token property">height</span><span class="token punctuation">:</span> <span class="token number">100%</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token selector">//==========================================================
// 這邊是新增的legend
// 定義 legend要長多大，要不要外框
<span class="token class">.legend</span> </span><span class="token punctuation">{</span>
  <span class="token property">line-height</span><span class="token punctuation">:</span> <span class="token number">18</span>px<span class="token punctuation">;</span>
  <span class="token property">color</span><span class="token punctuation">:</span> <span class="token hexcode">#555</span><span class="token punctuation">;</span>
  <span class="token property">background-color</span><span class="token punctuation">:</span> <span class="token hexcode">#FFFFFFBF</span><span class="token punctuation">;</span> //改底部顏色，最後兩碼是透明度
  <span class="token property">border-radius</span><span class="token punctuation">:</span> <span class="token number">5</span>px<span class="token punctuation">;</span> //邊角圓圓的好看
  <span class="token property">padding</span><span class="token punctuation">:</span> <span class="token number">10</span>px<span class="token punctuation">;</span> //決定padding的大小
  <span class="token property">box-shadow</span><span class="token punctuation">:</span> <span class="token number">0</span> <span class="token number">0</span> <span class="token number">15</span>px <span class="token function">rgba</span><span class="token punctuation">(</span><span class="token number">0</span>, <span class="token number">0</span>, <span class="token number">0</span>, <span class="token number">0.2</span><span class="token punctuation">)</span><span class="token punctuation">;</span> //加影子美觀
<span class="token punctuation">}</span>
<span class="token selector"><span class="token class">.legend</span> i </span><span class="token punctuation">{</span>
  <span class="token property">width</span><span class="token punctuation">:</span> <span class="token number">18</span>px<span class="token punctuation">;</span>
  <span class="token property">height</span><span class="token punctuation">:</span> <span class="token number">18</span>px<span class="token punctuation">;</span>
  <span class="token property">float</span><span class="token punctuation">:</span> left<span class="token punctuation">;</span>
  <span class="token property">margin-right</span><span class="token punctuation">:</span> <span class="token number">8</span>px<span class="token punctuation">;</span>
  <span class="token property">opacity</span><span class="token punctuation">:</span> <span class="token number">0.8</span><span class="token punctuation">;</span> //透明度選擇跟原本的圖一樣選<span class="token number">0.8</span>，這樣顏色才有辦法互相比對
<span class="token punctuation">}</span>

</code></pre>
<p>這樣就完成第一部分的作業了。</p>
<hr>
<h2 id="conditional-operators的簡化">Conditional Operators的簡化</h2>
<p>在此對<code>?</code>這個語法稍作解釋：這是一個if-else的簡化版<a href="https://stackoverflow.com/questions/2595392/what-does-the-question-mark-and-the-colon-ternary-operator-mean-in-objectiv">可以參考這裡</a>。基本上<code>?</code>前就是Ture-False判斷，<code>?</code>後就是if true要執行的code，<code>:</code>後是if false要執行的code。</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token comment">//所以以下這段code</span>
result <span class="token operator">=</span> <span class="token punctuation">(</span>a <span class="token operator">&gt;=</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token string">'positive'</span> <span class="token punctuation">:</span> <span class="token string">'negative or zero'</span><span class="token punctuation">;</span>
<span class="token comment">//同等於</span>
<span class="token keyword">if</span><span class="token punctuation">(</span>a <span class="token operator">&gt;=</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
 result <span class="token operator">=</span> <span class="token string">'positive'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
 result <span class="token operator">=</span> <span class="token string">'negative or zero'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>而以下的寫法就等於把一連串的if-else串起來，所以可以根據不同的數值來輸出顏色。</p>
<pre class=" language-javascript"><code class="prism = language-javascript"><span class="token keyword">function</span> <span class="token function">getColor</span><span class="token punctuation">(</span>d<span class="token punctuation">)</span><span class="token punctuation">{</span>
  <span class="token keyword">return</span> d <span class="token operator">&gt;</span> <span class="token number">5</span> <span class="token operator">?</span> <span class="token string">'#bd0026'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">4</span>  <span class="token operator">?</span> <span class="token string">'#f03b20'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">3</span>  <span class="token operator">?</span> <span class="token string">'#fd8d3c'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">2</span>  <span class="token operator">?</span> <span class="token string">'#feb24c'</span> <span class="token punctuation">:</span>
        d <span class="token operator">&gt;</span> <span class="token number">1</span>  <span class="token operator">?</span> <span class="token string">'#fed976'</span> <span class="token punctuation">:</span>
                  <span class="token string">'#ffffb2'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>

