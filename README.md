# brightcove

There could be various reasons why the loadedmetadata event is not getting called. Some common reasons include:

Cross-origin issues: If the video is hosted on a different domain than the page, there may be cross-origin issues that prevent the metadata from being loaded.
Incorrect event listener: Make sure that you have correctly added an event listener for the loadedmetadata event.
  Check if the syntax is correct and that the event listener is properly attached to the video element.
Slow network connection: If the network connection is slow, the metadata may take longer to load and 
  the loadedmetadata event may not fire until after a significant delay.
Video format not supported: If the video format is not supported by the browser, the loadedmetadata event may not fire.

It may be helpful to use the browser's developer tools to inspect the network requests and determine if there are any issues with loading the video's metadata.
If the issue still persists, you could try using a different event, such as canplay, which is fired when the video becomes ready to play.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Preloading the Brightcove script using the link tag with the rel="preload" attribute is a good practice to improve the performance of your page. 
It can potentially reduce the time it takes for the script to load and execute, which can improve the overall user experience.
However, preloading the script may not necessarily cause the loadedmetadata event to not fire.
It is possible that there are other factors, such as those mentioned in my previous response, that are affecting the event.
I would suggest checking the JavaScript console for any error messages and debugging the event listener for the loadedmetadata event to see if it is being properly attached and executed.
Additionally, you could try using a different event, such as canplay, to see if that resolves the issue.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The canplay and loadedmetadata events are both events that are fired by the HTML5 video element when it is ready to play. However, they have different meanings and are used for different purposes.
The loadedmetadata event is fired when the video's metadata, such as its dimensions, duration, and track list, have been loaded. 
This event occurs early in the video loading process and can be used to retrieve information about the video and make decisions about how to display it on the page.
The canplay event, on the other hand, is fired when the browser has determined that it can play the video without having to stop for buffering. 
This event occurs later in the video loading process and can be used to start playing the video when it is ready.
In general, if you want to wait until the video's metadata has loaded before performing an action, you should use the loadedmetadata event. 
If you want to wait until the video is ready to play without having to stop for buffering, you should use the canplay event.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Yes, that's correct. The canplay event is fired when the browser has determined that it has sufficient data to start playing the video without having to stop for buffering.
Prior to the canplay event firing, the browser will continue to load the video in the background to ensure that it has enough data to play smoothly.
It is important to note that the time it takes for the canplay event to fire can vary depending on various factors,
such as network conditions, the size of the video, and the capabilities of the device. However, once the canplay event has fired, 
you can be confident that the video is ready to play and can start playing it without having to worry about buffering interruptions.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

I see. So, you're using Brightcove player with Video.js, and you want to display the playlist separately in HTML and have a click event for the playlist items that starts playing the corresponding video in the player.
And you're using the loadedmetadata event to register the player instance globally, so that the playlist can access it.
If the loadedmetadata event is not firing as expected, it may prevent the playlist from accessing the player instance and cause issues with the playback.
To resolve this issue, you could try using a different event, such as canplay, which is fired when the video becomes ready to play.
Alternatively, you could try using a callback function to ensure that the playlist is only displayed once the player instance has been registered and is available for use.
If the issue persists, it may be helpful to use the browser's developer tools to inspect the JavaScript console for any error messages and debug the event listener and callback function to see if they are being properly executed.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#Player Issues

The issue with the click event not being called could be because the Brightcove player is preventing the event from bubbling up the DOM tree. 
To resolve this issue, you can try adding the click event listener to a different element within the player that does not have its own event handlers.
One option is to add the event listener to the vjs-poster element, which is the image displayed before the video starts playing:

```
var myPlayer = videojs.getPlayer('my-video');

myPlayer.ready(function() {
  var poster = myPlayer.el().getElementsByClassName('vjs-poster')[0];
  poster.addEventListener('click', function() {
    console.log('Clicked on video player');
  });
});
```

In this example, the poster variable is referencing the vjs-poster element within the player, and the click event listener is being added to this element.

Another option is to add the event listener directly to the video element:

```
var myPlayer = videojs.getPlayer('my-video');

myPlayer.ready(function() {
  var video = myPlayer.el().getElementsByTagName('video')[0];
  video.addEventListener('click', function() {
    console.log('Clicked on video player');
  });
});
```

In this example, the video variable is referencing the video element within the player, and the click event listener is being added to this element.
Try these solutions and see if they resolve the issue with the click event not being called.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

If the vjs-poster and vjs-overlay-screen elements are not working for you, you can try adding the click event listener directly to the player element:

```
var myPlayer = videojs.getPlayer('my-video');

myPlayer.ready(function() {
  var player = myPlayer.el();
  player.addEventListener('click', function() {
    console.log('Clicked on video player');
  });
});
```

In this example, the player variable is referencing the player element, and the click event listener is being added directly to this element.
If this solution also does not work, you may want to consider seeking additional help from the Brightcove player community 
or the Video.js community to troubleshoot the issue further.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

If the click event is only being called once after the video has been loaded, 
it's likely that the Brightcove player is using event bubbling to prevent further click events from being triggered. 
To resolve this issue, you can try using a different event, such as tap or touchstart, which are not prevented by event bubbling:

```
var myPlayer = videojs.getPlayer('my-video');

myPlayer.ready(function() {
  var player = myPlayer.el();
  player.addEventListener('touchstart', function() {
    console.log('Tapped on video player');
  });
});
```

In this example, the player variable is referencing the player element, and the touchstart event listener is being added directly to this element. 
When the player is tapped, the touchstart event will be triggered and the console.log statement will be executed.
Try this solution and see if it resolves the issue with the click event only being called once.
If the click event is only being called once after the video has been loaded, it's likely that the Brightcove player is using event bubbling to prevent further click events from being triggered.
To resolve this issue, you can try using a different event, such as tap or touchstart, which are not prevented by event bubbling:

```
var myPlayer = videojs.getPlayer('my-video');

myPlayer.ready(function() {
  var player = myPlayer.el();
  player.addEventListener('touchstart', function() {
    console.log('Tapped on video player');
  });
});
```

In this example, the player variable is referencing the player element, and the touchstart event listener is being added directly to this element. 
When the player is tapped, the touchstart event will be triggered and the console.log statement will be executed.
Try this solution and see if it resolves the issue with the click event only being called once.
