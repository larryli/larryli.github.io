---
ID: 642711
post_title: Javascript Mine
author: 南 靖男
post_date: 2009-10-14 23:37:44
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2009/10/642711
published: true
---
完全使用 JS 实现的扫雷。一个单 html 文件，直接下载保存就可以了。
<!--more-->
<code>
&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml"&gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" /&gt;
&lt;link rel="shortcut icon" href="data:image/x-icon;base64,AAABAAEAEBAAAAEAGABoAwAAFgAAACgAAAAQAAAAIAAAAAEAGAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACoWVWoWVUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACoWVXGlJ6eQEWLIh4AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACIJhCIJhCDGQuLIRyUNDGoWVWdPUGIHBSDGQuDGQuSMCiNKyAAAAAAAAAAAAAAAACrXWKTKyuWLzKWLzKWLzKdPUGbOj+MIyCLIRyHHBODFwmSMCgAAAAAAAAAAAAAAACcOT6cOT6gQEegQEefPkScOT6aNzyXMTWRJyeMIh2JIBmTNSkAAAAAAAAAAAAAAACgQ0qgQEepV2GpV2GpV2GoVV6fPkScOT6aNzyULS+MIx+JIBmLIh4AAAAAAACqW2SSKyuULS21cny1cny1cnykTlSRJyeRJyecOj+bOD2TLC6LIh6LIh4AAACuYGKVMS6YMjSjTU/CjpjCjpi+hI2oVVqTLiuNJiCqWWOhRUyaNzyZNDeLIBqrYljev8e4cnu4dH7Ci5POpq7TsLjJm6Tgxc2sXmSrXV+zbXapV2GkS1KkS1KkS1KSKicAAADOo6vXt77avcPeyM7eyc/dx8zQqbLAiZLCjpi3dX6vZG6pVl2kS1KkS1IAAAAAAADgxszZvsTiztPn19vp2t7l1dnhzNDXub/HmKG9g4yzb3moVV6kS1KkS1IAAAAAAAAAAADfys7n19vx5+nz7e/w5unm1trdx8zMo6zBjJW1cnyrXGakS1IAAAAAAAAAAAAAAAC2c33s3uH28fP8+/v07vDdwsjGlJjTsLjCjpi1cnysXmecPDgAAAAAAAAAAAAAAAC2c32kTFDy6ev28fP17u/TqrSdPUGRNS68hI21cnyqW2SLIhqqW2QAAAAAAAAAAACkTFDNoKIAAADw5+nn09fNnqmkTFC1dHzFlJ0AAACkS1KqW2QAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADw4+jOnqYAAAAAAAAAAAAAAAAAAAAAAAAAAAD+fwAA/D8AAMADAADAAwAAwAMAAMABAACAAQAAAAAAAAAAAACAAQAAgAEAAMADAADAAwAAwAEAAMgTAAD+fwAA" type="image/x-icon" /&gt;
&lt;title&gt;
JavaScript Mine - I Love Karen
&lt;/title&gt;
&lt;style type="text/css"&gt;
/*&lt;![CDATA[*/
html, body, * {
margin: 0 auto;
padding: 0;
font-family: Arial, Helvetica, Sans-serif;
}
h1, p {
text-align: center;
}
#minebox {
width: 500px;
height: 319px;
background-color: #c0c0c0;
-moz-user-select: none;
}
#minebox div, #minetable, #mineremain span, #mineface span, #minetimer span {
float: left;
}
#minelefttop, #mineleft, #mineleftbottom {
width: 12px;
}
#minerighttop, #mineright, #minerightbottom {
width: 8px;
}
#minelefttop, #minetop, #minerighttop {
height: 55px;
}
#mineleftbottom, #minebottom, #minerightbottom {
height: 8px;
}
#minetop, #minetable, #minebottom {
width: 480px;
}
#mineleft, #minetable, #mineright {
height: 256px;
}
#minelefttop, #minerighttop, #minetable td, #mineleftbottom, #minerightbottom,
#mineremain, #mineface, #minetimer, #mineremain span, #mineface span, #minetimer span {
background-image: url(data:image/gif;base64,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);
}
#minelefttop {
background-position: -166px -16px;
}
#minerighttop {
background-position: -178px -16px;
}
#mineleftbottom {
background-position: -166px -71px;
}
#minerightbottom {
background-position: -178px -71px;
}
#minetop, #minebottom {
background-image: url(data:image/gif;base64,R0lGODlhAQA3AJEAAP///76+voKCggAAACH5BAAHAP8ALAAAAAABADcAAAIKhIMpku0P43FLFAA7);
background-repeat: repeat-x;
}
#mineleft, #mineright {
background-image: url(data:image/gif;base64,R0lGODlhDAABAJEAAP///76+voKCggAAACH5BAAHAP8ALAAAAAAMAAEAAAIEhIMpWwA7);
background-repeat: repeat-y;
}
#mineremain, #mineface, #minetimer {
margin-top: 14px;
}
#mineremain, #minetimer {
width: 41px;
height: 25px;
background-position: -128px 0px;
}
#mineremain {
margin-left: 5px;
}
#mineface, #minetimer {
margin-left: 181px;
}
#mineface {
width: 26px;
height: 26px;
background-position: -128px -25px;
}
#mineremain span, #mineface span, #minetimer span {
display: block;
margin-top: 1px;
}
#mineremain1, #minefacebutton, #minetimer1 {
margin-left: 1px;
}
#mineremain span, #minetimer span {
width: 13px;
height: 23px;
}
.minenumber- {
background-position: 0px -56px;
}
.minenumber0 {
background-position: -26px -56px;
}
.minenumber1 {
background-position: -39px -56px;
}
.minenumber2 {
background-position: -52px -56px;
}
.minenumber3 {
background-position: -64px -56px;
}
.minenumber4 {
background-position: -77px -56px;
}
.minenumber5 {
background-position: -90px -56px;
}
.minenumber6 {
background-position: -103px -56px;
}
.minenumber7 {
background-position: -116px -56px;
}
.minenumber8 {
background-position: -129px -56px;
}
.minenumber9 {
background-position: -142px -56px;
}
#mineface span {
width: 24px;
height: 24px;
}
.minefaceclick {
background-position: 0px -32px;
}
.minefacewin {
background-position: -24px -32px;
}
.minefacefailed {
background-position: -48px -32px;
}
.minefacewoo {
background-position: -72px -32px;
}
.minefacesmile {
background-position: -96px -32px;
}
#minebox td {
width: 16px;
height: 16px;
}
.mineblock {
background-position: 0 0;
}
.minemark,
.mine80, .mine81, .mine82, .mine83, .mine84, .mine85, .mine86, .mine87, .mine88 {
background-position: -16px 0;
}
.mineunkown {
background-position: -32px 0;
}
.mineboom {
background-position: -48px 0;
}
.minewrong,
.mine64, .mine65, .mine66, .mine67, .mine68, .mine69, .mine70, .mine71, .mine72 {
background-position: -64px 0;
}
.minemine,
.mine16, .mine17, .mine18, .mine19, .mine20, .mine21, .mine22, .mine23, .mine24,
.mine144, .mine145, .mine146, .mine147, .mine148, .mine149, .mine150, .mine151, .mine152 {
background-position: -80px 0;
}
.mineunkown2 {
background-position: -96px 0;
}
.minenone, .mine0, .mine32, .mine128 {
background-position: -112px 0;
}
.mine1, .mine129 {
background-position: 0 -16px;
}
.mine2, .mine130 {
background-position: -16px -16px;
}
.mine3, .mine131 {
background-position: -32px -16px;
}
.mine4, .mine132 {
background-position: -48px -16px;
}
.mine5, .mine133 {
background-position: -64px -16px;
}
.mine6, .mine134 {
background-position: -80px -16px;
}
.mine7, .mine135 {
background-position: -96px -16px;
}
.mine8, .mine136 {
background-position: -112px -16px;
}
/*]]&gt;*/
&lt;/style&gt;
&lt;script type="text/javascript"&gt;
//&lt;![CDATA[
var $ = function(id) {
return document.getElementById(id);
}
var Mine = {
size: 16,
thetype: -1,
hasunkown: true,
enhanced: false,
setcookie: false,
def: [{    cols: 9, rows: 9, mine: 10 }, { cols: 16, rows: 16, mine: 40 }, { cols: 30, rows: 16, mine: 99 }],
stacksize: 720,    // 24x30=720 max
stackinit: function() {
Mine.stack = new Array(Mine.stacksize);
},
stackempty: function() {
Mine.stack = [];
Mine.stackpointer = 0;
},
stackpop: function(){
if (Mine.stackpointer &gt; 0) {
Mine.stackpointer--;
var p = Mine.stack[Mine.stackpointer];
var x = Math.floor(p / Mine.rows);
var y = p % Mine.rows;
return {x:x, y:y};
}
return 0;
},
stackpush: function(x, y) {
if (Mine.stackpointer &lt; Mine.stacksize){
Mine.stack[Mine.stackpointer] = Mine.rows * x + y;
Mine.stackpointer++;
return true;
}
return false;
},
init: function(n) {
Mine.stackinit();
Mine.tests = new Array(8);
Mine.start(n);
},
start: function(n) {
if (n != Mine.thetype) {
if (n &lt; 0 &amp;&amp; n &gt;= Mine.def.length)
n = 0;
Mine.thetype = n;
Mine.cols = Mine.def[n].cols;
Mine.maxx = Mine.cols - 1;
Mine.rows = Mine.def[n].rows;
Mine.maxy = Mine.rows - 1;
Mine.all = Mine.cols * Mine.rows;
Mine.mine = Mine.def[n].mine;
Mine.setbox();
}
Mine.remain = Mine.mine;
Mine.timer = Mine.opened = 0;
Mine.timerhandle = 0;
Mine.lastdown = 0;
Mine.testmark = Mine.testdown = 0;
Mine.isdown = 0;
Mine.isover = false;
Mine.settable();
Mine.setmines();
Mine.showremain();
Mine.showtimer();
Mine.face('smile');
$('minefacebutton').onmousedown = function() { Mine.face('click'); };
$('minefacebutton').onmouseup = function() {
var type = document.forms['mineform'].elements['type'];
for (var i = 0; i &lt; type.length; i++)
if (type[i].checked)
return Mine.reset(type[i].value);
};
},
reset: function(n) {
if (Mine.timerhandle)
window.clearInterval(Mine.timerhandle);
var len = $('minetable').childNodes.length;
for (var i = 0; i &lt; len; i++)
$('minetable').removeChild($('minetable').childNodes[0]);
Mine.start(n);
},
setunkown: function(hasunkown) {
Mine.hasunkown = (hasunkown) ? true : false;
},
setenhanced: function(enhanced) {
Mine.enhanced = (enhanced) ? true : false;
},
setbox: function() {
$('minetop').style.width = $('minetable').style.width = $('minebottom').style.width = (Mine.size * Mine.cols) + 'px';
$('mineleft').style.height = $('minetable').style.height = $('mineright').style.height = (Mine.size * Mine.rows) + 'px';
$('mineface').style.marginLeft = $('minetimer').style.marginLeft = ((Mine.size * Mine.cols - $('mineremain').clientWidth - $('mineface').clientWidth - $('minetimer').clientWidth - ($('mineremain').offsetLeft - $('minetop').offsetLeft) * 2) / 2) + 'px';
$('minebox').style.width = ($('mineleft').clientWidth + Mine.size * Mine.cols + $('mineright').clientWidth) + 'px';
$('minebox').style.height = ($('minetop').clientHeight + Mine.size * Mine.rows + $('minebottom').clientHeight) + 'px';
},
settable: function() {
Mine.mines = new Array();
for (var y = 0; y &lt; Mine.rows; y++) {
var tr = document.createElement('tr');
Mine.mines[y] = new Array();
for (var x = 0; x &lt; Mine.cols; x++) {
var td = document.createElement('td');
td.className = 'mineblock';
td.id = 'mine_' + y + '_' + x;
tr.appendChild(td);
Mine.mines[y][x] = 0;
}
$('minetable').appendChild(tr);
}
$('minetable').onmousemove = Mine.mousemove;
$('minetable').onmouseout = Mine.mouseout;
$('minetable').onmousedown = Mine.mousedown;
$('minetable').onmouseup = Mine.mouseup;
},
/*
* 000xxxxx 0  1  2  3  4  5  6  7   8 none
* 000xxxxx 10 11 12 13 14 15 16 17 18 mime
* 001xxxxx 20                         open
* 001xxxxx 30                         boom
* 010xxxxx 40 41 42 43 44 45 46 47 48 mark error
* 010xxxxx 50 51 52 53 54 55 56 57 58 mark vaild
* 100xxxxx 80 81 82 83 84 85 86 87 88 mark unkown none
* 110xxxxx 90 91 92 93 94 95 96 97 98 mark unkown mine
*/
setmines: function() {
for (var n = 0; n &lt; Mine.mine; n++) {
var x, y;
do {
x = Math.round(Math.random() * (Mine.maxx));
y = Math.round(Math.random() * (Mine.maxy));
} while (Mine.ismine(x, y));
Mine.mines[y][x] |= 0x10;
if (y &gt; 0) {
Mine.mines[y - 1][x]++;
if (x &gt; 0)
Mine.mines[y - 1][x - 1]++;
if (x &lt; Mine.maxx)
Mine.mines[y - 1][x + 1]++;
}
if (x &gt; 0)
Mine.mines[y][x - 1]++;
if (x &lt; Mine.maxx)
Mine.mines[y][x + 1]++;
if (y &lt; Mine.maxy) {
Mine.mines[y + 1][x]++;
if (x &gt; 0)
Mine.mines[y + 1][x - 1]++;
if (x &lt; Mine.maxx)
Mine.mines[y + 1][x + 1]++;
}
}
},
isblock: function (x, y) {
if (!(Mine.mines[y][x] &amp; 0xe0))
return true;
return false;
},
isunkown: function (x, y) {
if (Mine.mines[y][x] &amp; 0x80)
return true;
return false;
},
ismark: function (x, y) {
if (Mine.mines[y][x] &amp; 0x40)
return true;
return false;
},
isopened: function (x, y) {
if (Mine.mines[y][x] &amp; 0x20)
return true;
return false;
},
istips: function (x, y) {
if (Mine.mines[y][x] != 0 &amp;&amp; !(Mine.mines[y][x] &amp; 0xf0))
return true;
return false;
},
isopenedtips: function (x, y) {
if (Mine.mines[y][x] != 0 &amp;&amp; Mine.mines[y][x] &amp; 0x20)
return true;
return false;
},
isnone: function (x, y) {
if (Mine.mines[y][x] == 0)
return true;
return false;
},
ismine: function (x, y) {
if (Mine.mines[y][x] &amp; 0x10)
return true;
return false;
},
isunboom: function (x, y) {
if (((Mine.mines[y][x] &amp; 0x10) &amp;&amp; !(Mine.mines[y][x] &amp; 0x40)) || (!(Mine.mines[y][x] &amp; 0x10) &amp;&amp; (Mine.mines[y][x] &amp; 0x40)))
return true;
return false;
},
downpop: function() {
if (Mine.lastdown &gt; 0) {
var p = Mine.lastdown - 1;
var x = Math.floor(p / Mine.rows);
var y = p % Mine.rows;
$('mine_' + y + '_' + x).className = 'mineblock';
Mine.lastdown = 0;
return true;
}
return false;
},
downpush: function(x, y) {
if (Mine.lastdown == 0){
$('mine_' + y + '_' + x).className = 'minenone';
Mine.lastdown = Mine.rows * x + y + 1;
return true;
}
return false;
},
testpop2: function(){
if (Mine.testdown &gt; 0) {
Mine.testdown--;
var p = Mine.tests[Mine.testdown];
var x = Math.floor(p / Mine.rows);
var y = p % Mine.rows;
return {x:x, y:y};
}
return 0;
},
testpop: function(){
var popped;
while (popped = Mine.testpop2())
$('mine_' + popped.y + '_' + popped.x).className = 'mineblock';
},
testpush3: function(x, y) {
if (Mine.testdown &lt; 8){
$('mine_' + y + '_' + x).className = 'minenone';
Mine.tests[Mine.testdown] = Mine.rows * x + y;
Mine.testdown++;
return true;
}
return false;
},
testpush2: function(x ,y) {
if (Mine.isblock(x, y))
Mine.testpush3(x, y)
else if (Mine.ismark(x, y))
Mine.testmark++;
},
testpush: function(x, y) {
Mine.testmark = Mine.testdown = 0;
if (y &gt; 0) {
Mine.testpush2(x, y - 1);
if (x &gt; 0)
Mine.testpush2(x - 1, y - 1);
if (x &lt; Mine.maxx)
Mine.testpush2(x + 1, y - 1);
}
if (x &gt; 0)
Mine.testpush2(x - 1, y);
if (x &lt; Mine.maxx)
Mine.testpush2(x + 1, y);
if (y &lt; Mine.maxy) {
Mine.testpush2(x, y + 1);
if (x &gt; 0)
Mine.testpush2(x - 1, y + 1);
if (x &lt; Mine.maxx)
Mine.testpush2(x + 1, y + 1);
}
},
getmouse: function(event) {
var btn;
if (event == null) {
event = window.event;
switch (event.button) {
case 1:
btn = 0;
break;
case 4:
btn = 1;
break;
default:
btn = 2;
break;
}
} else
btn = event.button;
return {
x: event.clientX,
y: event.clientY,
b: btn
};
},
mousemove: function(event) {
if (Mine.isdown) {
m = Mine.getmouse(event);
var x = Math.floor((m.x - this.offsetLeft) / Mine.size);
var y = Math.floor((m.y - this.offsetTop) / Mine.size);
if (Mine.isdown &gt; 1) {
Mine.testpop();
if (Mine.isblock(x, y) || Mine.isopenedtips(x, y))
Mine.testpush(x, y);
} else {
Mine.downpop();
if (Mine.isblock(x, y))
Mine.downpush(x, y);
}
}
},
mouseout: function(event) {
if (Mine.isdown) {
if (Mine.isdown &gt; 1)
Mine.testpop();
else
Mine.downpop();
}
},
mousedown: function(event) {
var m;
if (Mine.timer == 1) {
Mine.showtimer();
Mine.timerhandle = window.setInterval(Mine.showtimer, 1000);
}
Mine.isdown++;
m = Mine.getmouse(event);
if (Mine.isdown &gt; 1) {
m.b = 1;
Mine.downpop();
}
var x = Math.floor((m.x - this.offsetLeft) / Mine.size);
var y = Math.floor((m.y - this.offsetTop) / Mine.size);
Mine.face('woo');
if (m.b == 0) {
if (Mine.isblock(x, y))
Mine.downpush(x, y);
else if (Mine.enhanced &amp;&amp; Mine.isopenedtips(x, y)) {
Mine.isdown++;
Mine.testpush(x, y);
}
} else if (m.b == 1 &amp;&amp; (Mine.isblock(x, y) || Mine.isopenedtips(x, y)))
Mine.testpush(x, y);
},
mouseup: function(event) {
Mine.isdown--;
m = Mine.getmouse(event);
if (Mine.isdown != 0) {
if (Mine.isdown &gt; 0)
m.b = 1;
else
Mine.face('smile');
Mine.isdown = 0;
}
var x = Math.floor((m.x - this.offsetLeft) / Mine.size);
var y = Math.floor((m.y - this.offsetTop) / Mine.size);
Mine.downpop();
switch (m.b) {
case 0:
Mine.open(x, y);
break;
case 1:
Mine.test(x, y);
break;
case 2:
Mine.mark(x, y);
break;
}
},
face: function(name) {
$('minefacebutton').className = 'mineface' + name;
},
showremain: function() {
var n = Mine.remain;
if (n &lt; 0) {
$('mineremain1').className = 'minenumber-';
n = -n;
for (var i = 3; i &gt; 1; i--) {
$('mineremain'+i).className = 'minenumber' + (n % 10);
n = Math.floor(n / 10);
}
} else
for (var i = 3; i &gt; 0; i--) {
$('mineremain'+i).className = 'minenumber' + (n % 10);
n = Math.floor(n / 10);
}
},
showtimer: function() {
if (Mine.timer &gt; 999) {
window.clearInterval(Mine.timerhandle);
Mine.timerhandle = 0;
} else {
var n = Mine.timer;
for (var i = 3; i &gt;= 1; i--) {
$('minetimer'+i).className = 'minenumber' + (n % 10);
n = Math.floor(n / 10);
}
Mine.timer++;
}
},
show: function(x, y) {
$('mine_' + y + '_' + x).className = 'mine' + Mine.mines[y][x];
Mine.mines[y][x] |= 0x20;
Mine.opened++;
},
boom: function(x, y) {
$('mine_' + y + '_' + x).className = 'mineboom';
Mine.mines[y][x] = 0x70;
Mine.isover = true;
},
over: function(iswin) {
$('minetable').onmouseover = function() { };
$('minetable').onmouseout = function() { };
$('minetable').onmousedown = function() { };
$('minetable').onmouseup = function() { };
if (Mine.timerhandle)
window.clearInterval(Mine.timerhandle);
if (iswin) {
Mine.face('win');
for (var y = 0; y &lt; Mine.rows; y++) {
for (var x = 0; x &lt; Mine.cols; x++) {
if (!Mine.isopened(x, y))
$('mine_' + y + '_' + x).className = 'minemark';
}
Mine.remain = 0;
Mine.showremain();
}
if (Mine.setcookie)
App.saved(Mine.thetype, Mine.timer - 1);
} else {
Mine.face('failed');
for (var y = 0; y &lt; Mine.rows; y++) {
for (var x = 0; x &lt; Mine.cols; x++) {
if (Mine.isunboom(x, y))
Mine.show(x, y);
}
}
}
},
check: function() {
if (Mine.isover)
Mine.over(false);
else if (Mine.opened + Mine.mine &gt;= Mine.all)
Mine.over(true);
else
Mine.face('smile');
},
mark: function(x, y) {
if (Mine.isblock(x, y)) {
$('mine_' + y + '_' + x).className = 'minemark';
Mine.mines[y][x] |= 0x40;
Mine.remain--;
Mine.showremain();
} else if (Mine.ismark(x, y)) {
if (Mine.hasunkown) {
$('mine_' + y + '_' + x).className = 'mineunkown';
Mine.mines[y][x] += 0x40;
} else {
$('mine_' + y + '_' + x).className = 'mineblock';
Mine.mines[y][x] &amp;= 0x1f;
}
Mine.remain++;
Mine.showremain();
} else if (Mine.isunkown(x, y)) {
$('mine_' + y + '_' + x).className = 'mineblock';
Mine.mines[y][x] &amp;= 0x1f;
}
Mine.face('smile');
},
test: function (x, y) {
if (Mine.isopenedtips(x, y)) {
var tipsblock = Mine.mines[y][x] - 0x20;
if (tipsblock == Mine.testmark) {
var popped;
while (popped = Mine.testpop2())
Mine.open2(popped.x, popped.y);
Mine.check();
return;
} else if (Mine.enhanced &amp;&amp; tipsblock == Mine.testmark + Mine.testdown ) {
var popped;
while (popped = Mine.testpop2())
Mine.mark(popped.x, popped.y);
Mine.check();
return;
}
}
Mine.testpop();
Mine.face('smile');
},
open: function (x, y) {
if (Mine.enhanced &amp;&amp; Mine.isopenedtips(x, y))
return Mine.test(x, y);
if (!Mine.isblock(x, y))
return Mine.face('smile');
Mine.open2(x, y);
Mine.check();
},
open2: function (x, y) {
if (Mine.ismine(x, y))
Mine.boom(x, y);
else if (Mine.istips(x, y))
Mine.show(x, y);
else{
var popped;
var left, right;</code>

Mine.stackempty();
if (!Mine.stackpush(x, y))
return;
while (popped = Mine.stackpop()) {
x = popped.x;
y = popped.y;
while ((y &gt;= 0) &amp;&amp; Mine.isnone(x, y))
y--;
y++;
left = right = 0;
if (y &gt; 0) {
if (Mine.istips(x, y - 1))
Mine.show(x, y - 1);
if (x &gt; 0)
if (Mine.isnone(x - 1, y - 1)) {
if (!Mine.stackpush(x - 1, y - 1))
return;
} else if(Mine.istips(x - 1, y - 1))
Mine.show(x - 1, y - 1);
if (x &lt; Mine.maxx)
if (Mine.isnone(x + 1, y - 1)) {
if (!Mine.stackpush(x + 1, y - 1))
return;
} else if (Mine.istips(x + 1, y - 1))
Mine.show(x + 1, y - 1);
}
while ((y &lt; Mine.rows) &amp;&amp; Mine.isnone(x, y)) {
Mine.show(x, y);
if (x &gt; 0) {
if (!left &amp;&amp; Mine.isnone(x - 1, y)) {
if (!Mine.stackpush(x - 1, y))
return;
left = 1;
} else {
if (left &amp;&amp; !Mine.isnone(x - 1, y))
left = 0;
if (Mine.istips(x - 1, y))
Mine.show(x - 1, y);
}
}
if (x &lt; Mine.maxx) {
if (!right &amp;&amp; Mine.isnone(x + 1, y)) {
if (!Mine.stackpush(x + 1, y))
return;
right = 1;
} else {
if (right &amp;&amp; !Mine.isnone(x + 1, y))
right = 0;
if (Mine.istips(x + 1, y))
Mine.show(x + 1, y);
}
}
y++;
}
if (y &lt; Mine.rows) {
if (Mine.istips(x, y))
Mine.show(x, y);
if (x &gt; 0)
if (Mine.isnone(x - 1, y)) {
if (!Mine.stackpush(x - 1, y))
return;
} else if (Mine.istips(x - 1, y))
Mine.show(x - 1, y);
if (x &lt; Mine.maxx)
if (Mine.isnone(x + 1, y)) {
if (!Mine.stackpush(x + 1, y))
return;
} else if (Mine.istips(x + 1, y))
Mine.show(x + 1, y);
}
}
}
},
};
var Cookie = {
test: function() {
var hi = 'ILoveSzeSze';
Cookie.set(hi, 1);
var ret = Cookie.get(hi);
if (ret != 1)
return false;
Cookie.unset(hi);
return true;
},
get: function(key) {
tmp = document.cookie.match((new RegExp(key + '=[a-zA-Z0-9.()-=|%/]+($|;)', 'g')));
if (!tmp || !tmp[0])
return '';
else
return unescape(tmp[0].substring(key.length + 1, tmp[0].length).replace(';', '')) || null;
},
set: function(key, value, ttl, path, domain, secure) {
cookie = [key + '=' + escape(value), 'path=' + ((!path || path == '') ? '/' : path), 'domain=' + ((!domain || domain == '') ?  window.location.hostname : domain)];
if (ttl)
cookie.push('expires=' + Cookie._hourstodate(ttl));
if (secure)
cookie.push('secure');
return document.cookie = cookie.join('; ');
},
unset: function(key, path, domain) {
path = (!path || typeof path != 'string') ? '' : path;
domain = (!domain || typeof domain != 'string') ? '' : domain;
if (Cookie.get(key))
Cookie.set(key, '', 'Thu, 01-Jan-70 00:00:01 GMT', path, domain);
},
_hourstodate: function(ttl) {
if (parseInt(ttl) == 'NaN' )
return '';
else {
now = new Date();
now.setTime(now.getTime() + (parseInt(ttl) * 60 * 60 * 1000));
return now.toGMTString();
}
}
}
var App = {
tips: "Level %snPlease input your name:",
sec: ' secends',
none: 'No record',
saved: function(type, time) {
var last = parseInt(Cookie.get('jsmine' + type));
if (isNaN(last) || last &lt;= 0 || time &lt; last) {
var types = $('type').getElementsByTagName('label');
var name = Cookie.get('jsmine' + type + 'name');
var tips = App.tips.replace('%s',types[type].innerHTML);
do {
name = window.prompt(tips, name);
if (name == null)
return;
} while (name.length &lt;= 0 &amp;&amp; name.length &gt; 32);
Cookie.set('jsmine' + type, time, 13140);
Cookie.set('jsmine' + type + 'name', name, 13140);
}
},
show: function() {
var types = $('type').getElementsByTagName('label');
var text = $('scoreboard').value + "nn";
for (var i = 0; i &lt; types.length; i++) {
var time = Cookie.get('jsmine' + i);
if (time != '')
time += App.sec + "t " + Cookie.get('jsmine' + i + 'name');
else
time = App.none;
text += types[i].innerHTML + ":t " + time + "n";
}
window.alert(text);
},
start: function() {
if (Cookie.test()) {
Mine.setcookie = true;
$('scoreboard').style.display = '';
}
var type = document.forms['mineform'].elements['type'];
var href = window.location.href;
var index = href.lastIndexOf('?');
if (index != '-1') {
var query = href.substr(index + 1);
var querys = query.split("&amp;");
for (var i = 0; i&lt; querys.length; i++) {
var value = querys[i].split('=');
var n = parseInt(value[1]);
switch (value[0]) {
case 'type':
if (n &gt;= 0 &amp;&amp; n &lt; type.length)
type[n].checked = true;
break;
case 'unkown':
$('unkown').checked = (n == 1);
break;
case 'enhanced':
$('enhanced').style.display = $('enhancedversion').style.display ='';
$('enhanced').checked = (n == 1);
break;
}
}
}
Mine.setunkown($('unkown').checked);
Mine.setenhanced($('enhanced').checked);
for (var i = 0; i &lt; type.length; i++)
if (type[i].checked)
break;
Mine.init(type[i].value);
},
disable: function() {
document.oncontextmenu = function(event) {
if (event == null)
event = window.event;
event.returnValue = false;
return false;
};
},
language: function() {
var lang;
if (navigator.appName == 'Netscape')
lang = navigator.language.toLowerCase();
else
lang = navigator.browserLanguage.toLowerCase();
switch (lang) {
case 'zh-cn':
case 'zh-sg':
$('title').innerHTML = '网页扫雷';
document.title = $('title').innerHTML + ' - 我爱思思';
var types = $('type').getElementsByTagName('label');
types[0].innerHTML = '初级';
types[1].innerHTML = '中级';
types[2].innerHTML = '高级';
$('markunkown').innerHTML = '标记(?)';
$('enhancedversion').innerHTML = '加强版';
$('copyright').innerHTML = '版权所有';
$('scoreboard').value = '扫雷英雄榜';
App.tips = "已破%s记录。n请留尊姓大名。";
App.sec = '秒';
App.none = '没有记录';
break;
case 'zh-tw':
case 'zh-hk':
$('title').innerHTML = '網頁踩地雷';
document.title = $('title').innerHTML + ' - 我愛思思';
var types = $('type').getElementsByTagName('label');
types[0].innerHTML = '初級';
types[1].innerHTML = '中級';
types[2].innerHTML = '高級';
$('markunkown').innerHTML = '標記(?)';
$('enhancedversion').innerHTML = '增強版';
$('copyright').innerHTML = '版權所有';
$('scoreboard').value = '踩雷英雄榜';
App.tips = "已破%s記錄。n請留尊姓大名。";
App.sec = '秒';
App.none = '尚未有記錄';
break;
}
},
init: function() {
App.disable();
App.language();
App.start();
}
}
//]]&gt;
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h1 id="title"&gt;
JavaScript Mine
&lt;/h1&gt;
&lt;form action="GET" name="mineform"&gt;
&lt;p id="type"&gt;
&lt;input type="radio" name="type" value="0" onclick="Mine.reset(0)" /&gt;
&lt;label&gt;Beginner&lt;/label&gt;
&lt;input type="radio" name="type" value="1" onclick="Mine.reset(1)" /&gt;
&lt;label&gt;Normal&lt;/label&gt;
&lt;input type="radio" name="type" value="2" checked="true" onclick="Mine.reset(2)" /&gt;
&lt;label&gt;Expert&lt;/label&gt;
&lt;/p&gt;
&lt;p&gt;
&lt;input type="checkbox" id="unkown" name="unkown" value="1" onclick="Mine.setunkown(this.checked)" /&gt;
&lt;label id="markunkown"&gt;Mark Unkown(?)&lt;/label&gt;
&lt;input type="checkbox" id="enhanced" name="enhanced" value="1" onclick="Mine.setenhanced(this.checked)" style="display: none;" /&gt;
&lt;label id="enhancedversion" style="display: none;"&gt;Enhanced Version&lt;/label&gt;
&lt;/p&gt;
&lt;/form&gt;
&lt;div id="minebox"&gt;
&lt;div id="minelefttop"&gt;&lt;/div&gt;
&lt;div id="minetop"&gt;
&lt;div id="mineremain"&gt;
&lt;span id="mineremain1" class="minenumber0"&gt;&lt;/span&gt;&lt;span id="mineremain2" class="minenumber0"&gt;&lt;/span&gt;&lt;span id="mineremain3" class="minenumber0"&gt;&lt;/span&gt;
&lt;/div&gt;
&lt;div id="mineface"&gt;
&lt;span id="minefacebutton" class="minefacesmile"&gt;&lt;/span&gt;
&lt;/div&gt;
&lt;div id="minetimer"&gt;
&lt;span id="minetimer1" class="minenumber0"&gt;&lt;/span&gt;&lt;span id="minetimer2" class="minenumber0"&gt;&lt;/span&gt;&lt;span id="minetimer3" class="minenumber0"&gt;&lt;/span&gt;
&lt;/div&gt;
&lt;/div&gt;
&lt;div id="minerighttop"&gt;&lt;/div&gt;
&lt;div id="mineleft"&gt;&lt;/div&gt;
&lt;table id="minetable" cellpadding="0" cellspacing="0"&gt;&lt;/table&gt;
&lt;div id="mineright"&gt;&lt;/div&gt;
&lt;div id="mineleftbottom"&gt;&lt;/div&gt;
&lt;div id="minebottom"&gt;&lt;/div&gt;
&lt;div id="minerightbottom"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;p&gt;
&lt;span id="copyright"&gt;Copyright&lt;/span&gt; &amp;copy; 2009 &lt;a href="https://larryli.cn/" title="Larry Li's Weblog"&gt;Larry Li&lt;/a&gt;. Ver 0.03
&lt;input type="button" id="scoreboard" name="" value="Score Board" onclick="App.show();" style="display:none;" /&gt;
&lt;/p&gt;
&lt;script type="text/javascript"&gt;
//&lt;![CDATA[
App.init();
//]]&gt;
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;