# TRANSMUTE v1

## HTML

```.html
<!DOCTYPE html>
<html><head>
    <title>TRANSMUTE</title>
</head><body>
    <h1 class="heading"><small>transmute</small></h1>
    <input class="URL-input" placeholder="URL: https://www.youtube.com/watch?v=MtN1YnoL46Q">
    <button class="convert-button">Transmute</button>
</body>
</html>
```
## CSS

```css
<link rel="stylesheet" href="style.css">
* {
    text-align: center;
}.heading {
    font-family: Arial;
    margin-top:40vh;
}.URL-input, .convert-button {
    font-size:1.3em;
    padding:5px 10px;
}.URL-input {
    border-radius:4px 0px 0px 4px;
    width:30em;
    text-align: left;
    border:2px solid #EEEEEE;
    background: #EEEEEE;
    outline:none;
}.URL-input:focus {
    border:2px solid #0485ff;
}.convert-button {
    border-radius:0px 4px 4px 0px;
    border:2px solid #0485ff;
    background: #0485ff;
    color:white;
}
```

## JavaScript and Node.js

```js
var convertBtn = document.querySelector('.convert-button');
var URLinput = document.querySelector('.URL-input');convertBtn.addEventListener('click', () => {
    console.log(`URL: ${URLinput.value}`);
    sendURL(URLinput.value);
});function sendURL(URL) {
    // We will put code here later
}
```

## NODE

```js
npm init
npm install express cors ytdl-core
```
ctrl+n file **index.js**

```js
const express = require('express');
const cors = require('cors');
const ytdl = require('ytdl-core');
const app = express();app.listen(4000, () => {
    console.log('Server Works !!! At port 4000');
});
```
**Run**
```js
node index.js
```
Add listen on request /path `/download`
```js
const express = require('express');
const cors = require('cors');
const ytdl = require('ytdl-core');
const app = express();app.use(cors());app.listen(4000, () => {
    console.log('Server Works !!! At port 4000');
});app.get('/download', (req,res) => {
    var URL = req.query.URL;
    res.json({url:URL});
})
```
GET request to server at `/download` respone + query = GET `fetch()`
```js
var convertBtn = document.querySelector('.convert-button');
var URLinput = document.querySelector('.URL-input');convertBtn.addEventListener('click', () => {
    console.log(`URL: ${URLinput.value}`);
    sendURL(URLinput.value);
});function sendURL(URL) {
    fetch(`http://localhost:4000/download?URL=${URL}`, {
        method:'GET'
    }).then(res => res.json())
    .then(json => console.log(json));
}
```
Server response `convertBtn.addEventListner('click', () => { console.log('URL: ${URLinput.value}'); sendURL(URLinput.value); });`
```js
var convertBtn = document.querySelector('.convert-button');
var URLinput = document.querySelector('.URL-input');convertBtn.addEventListener('click', () => {
    console.log(`URL: ${URLinput.value}`);
    sendURL(URLinput.value);
});function sendURL(URL) {
    window.location.href = `http://localhost:4000/download?URL=${URL}`;
}
```
**ytdl-core**
ytdl-core module can be installed in your node project. `ytdl.videoInfo` gives information about a video. ytdl validates Youtube URLs and validates Youtube video IDs
