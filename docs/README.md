# About
The Peloton web application does not display target metrics, like cadence and resistance. This bookmarklet uses the Peloton web application and API to display the target metrics. Works in cycling classes viwed in the browser only.

![Alt](https://i.ibb.co/NTyLcW8/pelokeiserbookmarklet.jpg "Peloton class with target metrics")

# Metrics
- Two resistance ranges are displayed. The first is for the Keiser bike, the second is for Peloton (in parentheses). Resistance conversion is based on [this commonly accepted conversion chart](https://www.sippingandshopping.org/wp-content/uploads/2019/04/Peloton-Keiser-Resistance-Conversion-Chart.jpg).
- Live and recently added classes do not have metrics. It can take a day or more for Peloton to add metrics to a recording.
- Metrics begin after the 1 minute warm-up.

# How to use
1. Start a cycling class on the Peloton website.
2. Open the PeloKeiser bookmark.
3. Metrics are magically displayed! (after the one minute start/warm-up)

To create a bookmark for PeloKeiser in your web browser, you will copy the entire code below and use it as the "URL" for your bookmark. 
```
javascript:(function(){var rideID=window.location.pathname.split("/");rideID=rideID[rideID.length-1],fetch("https://api.onepeloton.com/api/ride/"+rideID+"/details?stream_source=multichannel",{headers:{accept:"application/json, text/plain, */*","accept-language":"en-US","peloton-platform":"web","sec-fetch-dest":"empty","sec-fetch-mode":"cors","sec-fetch-site":"same-site","x-requested-with":"XmlHttpRequest"},referrer:"https://members.onepeloton.com/classes/player/"+rideID,referrerPolicy:"no-referrer-when-downgrade",body:null,method:"GET",mode:"cors",credentials:"include"}).then(function(e){return e.json()}).then(function(e){var t=[1,1,1,1,1,2,2,2,3,3,3,4,4,4,5,5,5,6,6,7,7,8,8,9,9,9,10,10,10,10,10,11,11,11,11,12,12,12,12,13,13,13,14,14,14,14,15,15,15,15,15,16,16,16,16,16,17,17,17,17,17,18,18,18,18,18,19,19,19,19,19,20,20,20,20,20,21,21,21,21,21,22,22,22,22,22,23,23,23,23,23,24,24,24,24,24,24,24,24,24,24],r=Number(e.ride.duration),n=document.createElement("div");n.id="cadresist",n.style="color:white",n.innerHTML='<div id="cadresisttxt" style="width:100%;color:white"></div><div style="margin-top:10px;width:100%; height:2px; background-color:#555555"><div id="cadresistprogress" style="width:0%;transition:990ms linear;height:2px;background-color:white"></div></div>',document.querySelector("div[data-test-id='videoSongContainer']").after(n);var s=document.getElementById("cadresisttxt"),i=document.getElementById("cadresistprogress");if(!e.instructor_cues.length)return n.innerHTML="Class does not have target metrics.",void setTimeout(function(){n.innerHTML=""},5e3);for(var a=[],o=e.instructor_cues[0],c=1;c<e.instructor_cues.length;c++){var d=e.instructor_cues[c];o.resistance_range.upper==d.resistance_range.upper&&o.resistance_range.lower==d.resistance_range.lower&&o.cadence_range.upper==d.cadence_range.upper&&o.cadence_range.lower==d.cadence_range.lower?o.offsets.end=d.offsets.end:(a.push(o),o=d)}a.push(d),e.instructor_cues=a;var u=document.querySelector("div[data-test-id='video-timer']");new MutationObserver(function(n){var a=document.querySelector("p[data-test-id='time-to-complete']");if(!a)return;if(2!=(a=a.innerHTML.split(":")).length)return;for(var o=r-(60*Number(a[0])+Number(a[1]))+Number(e.ride.pedaling_start_offset),c=0;c<e.instructor_cues.length;c++){var d=e.instructor_cues[c];if(o>=Number(d.offsets.start)&&o<=Number(d.offsets.end))return s.innerHTML="cadence: "+d.cadence_range.lower+" - "+d.cadence_range.upper+"&nbsp;&nbsp;&nbsp;&nbsp; resistance: "+t[d.resistance_range.lower]+" - "+t[d.resistance_range.upper]+"&nbsp;&nbsp;&nbsp;&nbsp; ("+d.resistance_range.lower+" - "+d.resistance_range.upper+")",void(o==Number(d.offsets.start)?(i.style.transition="none",i.style.width="0%"):(i.style.transition="990ms linear",i.style.width=Math.round((o-d.offsets.start)/(d.offsets.end-d.offsets.start)*100)+"%"))}}).observe(u,
{attributes:!0,childList:!0,subtree:!0,characterData:!0})});})();

```

## iPad
In Safari, create a new bookmark (to anything -- doesn't matter). Copy the PeloKeiser code above. In Safari, open the bookmarks side panel, find the new bookmark, replace the URL with the link you copied, and rename it to PeloKeiser. 

## iPhone
In Safari, create a new bookmark (to anything -- doesn't matter). Copy the PeloKeiser code above. Open your bookmarks, find the new bookmark, and replace the URL with the link you copied, and rename it to PeloKeiser. (Need more help? Google "iphone bookmarklet").

## Computer Web Browser
In your web browser, create a new bookmark in your to the bookmarks bar. Name it PeloKeiser and copy the PeloKeiser code above into the URL field.

## Safari on a Mac
In your web browser, create a new bookmark in your to the bookmarks bar. Name it PeloKeiser and copy the PeloKeiser code above into the URL field. If you do not see the bookmarks bar, go to the View menu and select "Show Favorites Bar".

## Chromebook
In your web browser, create a new bookmark in your to the bookmarks bar. Name it PeloKeiser and copy the PeloKeiser code above into the URL field.  Use Ctrl+Shift+B to reveal the bookmarks bar, if hidden.

Super special thanks to creator ZV3zrmCT who was generous enough to share their code after originally writing this project up with [Target Metrics and Schwinn IC4 Peloton resistance conversions](https://zv3zrmct.github.io/peloton_schwinn_metrics/).
