---
title: about
date: 2017-04-09 17:16:10
---

i'm a web developer born and raised in winnipeg, manitoba, currently living in montreal, quebec.  i completed my bachelors of science in mathematics at mcgill university in 2006 and studied web development after that at concordia university.

<!-- CV -->
[**→ curriculum vitae** (/kəˈrɪkjᵿləm ˈviːtaɪ/, /ˈwiːtaɪ/, or /ˈvaɪtiː/)](//cv.tenzin.ca)
<!-- /CV -->

<!-- CONTACT INFO -->
## contact information

phone : +1.514.815.8883
email : <a href="mailto:tenzin@tenzin.ca">tenzin[at]tenzin[dot]ca</a>

<!-- /CONTACT INFO -->

<!-- PROFILE PIC -->
here is an old picture of me
![alt text](../images/me.png "here is an old picture of me")
<!-- /PROFILE PIC -->

<!-- GOOGLE MAPS -->
<script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyBm8XpxrP2QYGkoUl7YFyBk8uIqjzWFGTc&extension=.js"></script>
<script src="https://cdn.mapkit.io/v1/infobox.js"></script>
<link href="https://fonts.googleapis.com/css?family=Roboto:300,400" rel="stylesheet">
<link href="https://cdn.mapkit.io/v1/infobox.css" rel="stylesheet" >

<script>
  google.maps.event.addDomListener(window, 'load', init);
  var map, markersArray = [];

  function bindInfoWindow(marker, map, location) {
  google.maps.event.addListener(marker, 'click', function() {
    function close(location) {
      location.ib.close();
      location.infoWindowVisible = false;
      location.ib = null;
    }

    if (location.infoWindowVisible === true) {
      close(location);
    } else {
      markersArray.forEach(function(loc, index){
        if (loc.ib && loc.ib !== null) {
          close(loc);
        }
      });

      var boxText = document.createElement('div');
      boxText.style.cssText = 'background: #fff;';
      boxText.classList.add('md-whiteframe-2dp');

      function buildPieces(location, el, part, icon) {
        if (location[part] === '') {
          return '';
        } else if (location.iw[part]) {
          switch(el){
            case 'photo':
              if (location.photo){
                return '<div class="iw-photo" style="background-image: url(' + location.photo + ');"></div>';
               } else {
                return '';
              }
              break;
            case 'iw-toolbar':
              return '<div class="iw-toolbar"><h3 class="md-subhead">' + location.title + '</h3></div>';
              break;
            case 'div':
              switch(part){
                case 'email':
                  return '<div class="iw-details"><i class="material-icons" style="color:#4285f4;"><img src="//cdn.mapkit.io/v1/icons/' + icon + '.svg"/></i><span><a href="mailto:' + location.email + '" target="_blank">' + location.email + '</a></span></div>';
                  break;
                case 'web':
                  return '<div class="iw-details"><i class="material-icons" style="color:#4285f4;"><img src="//cdn.mapkit.io/v1/icons/' + icon + '.svg"/></i><span><a href="' + location.web + '" target="_blank">' + location.web_formatted + '</a></span></div>';
                  break;
                case 'desc':
                  return '<label class="iw-desc" for="cb_details"><input type="checkbox" id="cb_details"/><h3 class="iw-x-details">Details</h3><i class="material-icons toggle-open-details"><img src="//cdn.mapkit.io/v1/icons/' + icon + '.svg"/></i><p class="iw-x-details">' + location.desc + '</p></label>';
                  break;
                default:
                  return '<div class="iw-details"><i class="material-icons"><img src="//cdn.mapkit.io/v1/icons/' + icon + '.svg"/></i><span>' + location[part] + '</span></div>';
                break;
              }
              break;
            case 'open_hours':
              var items = '';
              if (location.open_hours.length > 0){
                for (var i = 0; i < location.open_hours.length; ++i) {
                  if (i !== 0){
                    items += '<li><strong>' + location.open_hours[i].day + '</strong><strong>' + location.open_hours[i].hours +'</strong></li>';
                  }
                  var first = '<li><label for="cb_hours"><input type="checkbox" id="cb_hours"/><strong>' + location.open_hours[0].day + '</strong><strong>' + location.open_hours[0].hours +'</strong><i class="material-icons toggle-open-hours"><img src="//cdn.mapkit.io/v1/icons/keyboard_arrow_down.svg"/></i><ul>' + items + '</ul></label></li>';
                }
                return '<div class="iw-list"><i class="material-icons first-material-icons" style="color:#4285f4;"><img src="//cdn.mapkit.io/v1/icons/' + icon + '.svg"/></i><ul>' + first + '</ul></div>';
               } else {
                return '';
              }
              break;
           }
        } else {
          return '';
        }
      }

      boxText.innerHTML =
        buildPieces(location, 'photo', 'photo', '') +
        buildPieces(location, 'iw-toolbar', 'title', '') +
        buildPieces(location, 'div', 'address', 'location_on') +
        buildPieces(location, 'div', 'web', 'public') +
        buildPieces(location, 'div', 'email', 'email') +
        buildPieces(location, 'div', 'tel', 'phone') +
        buildPieces(location, 'div', 'int_tel', 'phone') +
        buildPieces(location, 'open_hours', 'open_hours', 'access_time') +
        buildPieces(location, 'div', 'desc', 'keyboard_arrow_down');

      var myOptions = {
        alignBottom: true,
        content: boxText,
        disableAutoPan: true,
        maxWidth: 0,
        pixelOffset: new google.maps.Size(-140, -40),
        zIndex: null,
        boxStyle: {
          opacity: 1,
          width: '280px'
        },
        closeBoxMargin: '0px 0px 0px 0px',
        infoBoxClearance: new google.maps.Size(1, 1),
        isHidden: false,
        pane: 'floatPane',
        enableEventPropagation: false
      };

      location.ib = new InfoBox(myOptions);
      location.ib.open(map, marker);
      location.infoWindowVisible = true;
    }
  });
  }

  function init() {
    var mapOptions = {
      center: new google.maps.LatLng(45.47289238859529,-73.58219251416017),
      zoom: 10,
      gestureHandling: 'none',
      fullscreenControl: false,
      zoomControl: false,
      disableDoubleClickZoom: false,
      mapTypeControl: false,
      scaleControl: false,
      scrollwheel: true,
      streetViewControl: false,
      draggable : true,
      clickableIcons: false,
      mapTypeId: google.maps.MapTypeId.ROADMAP,
      styles: [{"featureType":"all","elementType":"all","stylers":[{"visibility":"on"}]},{"featureType":"all","elementType":"labels","stylers":[{"visibility":"off"},{"saturation":"-100"}]},{"featureType":"all","elementType":"labels.text.fill","stylers":[{"saturation":36},{"color":"#000000"},{"lightness":40},{"visibility":"off"}]},{"featureType":"all","elementType":"labels.text.stroke","stylers":[{"visibility":"off"},{"color":"#000000"},{"lightness":16}]},{"featureType":"all","elementType":"labels.icon","stylers":[{"visibility":"off"}]},{"featureType":"administrative","elementType":"geometry.fill","stylers":[{"color":"#000000"},{"lightness":20}]},{"featureType":"administrative","elementType":"geometry.stroke","stylers":[{"color":"#000000"},{"lightness":17},{"weight":1.2}]},{"featureType":"landscape","elementType":"geometry","stylers":[{"color":"#000000"},{"lightness":20}]},{"featureType":"landscape","elementType":"geometry.fill","stylers":[{"color":"#4d6059"}]},{"featureType":"landscape","elementType":"geometry.stroke","stylers":[{"color":"#4d6059"}]},{"featureType":"landscape.natural","elementType":"geometry.fill","stylers":[{"color":"#4d6059"}]},{"featureType":"poi","elementType":"geometry","stylers":[{"lightness":21}]},{"featureType":"poi","elementType":"geometry.fill","stylers":[{"color":"#4d6059"}]},{"featureType":"poi","elementType":"geometry.stroke","stylers":[{"color":"#4d6059"}]},{"featureType":"road","elementType":"geometry","stylers":[{"visibility":"on"},{"color":"#7f8d89"}]},{"featureType":"road","elementType":"geometry.fill","stylers":[{"color":"#7f8d89"}]},{"featureType":"road.highway","elementType":"geometry.fill","stylers":[{"color":"#7f8d89"},{"lightness":17}]},{"featureType":"road.highway","elementType":"geometry.stroke","stylers":[{"color":"#7f8d89"},{"lightness":29},{"weight":0.2}]},{"featureType":"road.arterial","elementType":"geometry","stylers":[{"color":"#000000"},{"lightness":18}]},{"featureType":"road.arterial","elementType":"geometry.fill","stylers":[{"color":"#7f8d89"}]},{"featureType":"road.arterial","elementType":"geometry.stroke","stylers":[{"color":"#7f8d89"}]},{"featureType":"road.local","elementType":"geometry","stylers":[{"color":"#000000"},{"lightness":16}]},{"featureType":"road.local","elementType":"geometry.fill","stylers":[{"color":"#7f8d89"}]},{"featureType":"road.local","elementType":"geometry.stroke","stylers":[{"color":"#7f8d89"}]},{"featureType":"transit","elementType":"geometry","stylers":[{"color":"#000000"},{"lightness":19}]},{"featureType":"water","elementType":"all","stylers":[{"color":"#2b3638"},{"visibility":"on"}]},{"featureType":"water","elementType":"geometry","stylers":[{"color":"#2b3638"},{"lightness":17}]},{"featureType":"water","elementType":"geometry.fill","stylers":[{"color":"#24282b"}]},{"featureType":"water","elementType":"geometry.stroke","stylers":[{"color":"#24282b"}]},{"featureType":"water","elementType":"labels","stylers":[{"visibility":"off"}]},{"featureType":"water","elementType":"labels.text","stylers":[{"visibility":"off"}]},{"featureType":"water","elementType":"labels.text.fill","stylers":[{"visibility":"off"}]},{"featureType":"water","elementType":"labels.text.stroke","stylers":[{"visibility":"off"}]},{"featureType":"water","elementType":"labels.icon","stylers":[{"visibility":"off"}]}]
    }
    var mapElement = document.getElementById('mapkit-5897');
    var map = new google.maps.Map(mapElement, mapOptions);
    var locations = [
      {"title":"Montréal","address":"Montréal, QC, Canada","desc":"","tel":"","int_tel":"","email":"","web":"","web_formatted":"","open":"","time":"","lat":45.5016889,"lng":-73.56725599999999,"vicinity":"Montréal","open_hours":"","marker":{"url":"https://maps.gstatic.com/mapfiles/api-3/images/spotlight-poi_hdpi.png","scaledSize":{"width":25,"height":42,"j":"px","f":"px"},"origin":{"x":0,"y":0},"anchor":{"x":12,"y":42}},"iw":{"address":true,"desc":true,"email":true,"enable":true,"int_tel":true,"open":true,"open_hours":true,"photo":true,"tel":true,"title":true,"web":true}}
    ];
    for (i = 0; i < locations.length; i++) {
      marker = new google.maps.Marker({
        icon: locations[i].marker,
        position: new google.maps.LatLng(locations[i].lat, locations[i].lng),
        map: map,
        title: locations[i].title,
        address: locations[i].address,
        desc: locations[i].desc,
        tel: locations[i].tel,
        int_tel: locations[i].int_tel,
        vicinity: locations[i].vicinity,
        open: locations[i].open,
        open_hours: locations[i].open_hours,
        photo: locations[i].photo,
        time: locations[i].time,
        email: locations[i].email,
        web: locations[i].web,
        iw: locations[i].iw
      });
      markersArray.push(marker);

      if (locations[i].iw.enable === true){
        bindInfoWindow(marker, map, locations[i]);
      }
    }
  }
</script>

<style>
  #mapkit-5897 {
    height:300px;
    width:600px;
  }
  .gmnoprint {
    display:none;
  }
  .gm-style-cc {
    display:none;
  }
</style>

<div id='mapkit-5897'></div>
<!-- /GOOGLE MAPS -->