# study-share

# 直播中遇到的坑（）
1，自动播放的问题（autoplay存在兼容性问题）
```javascript
<script>
  if ("wView" in window) {
    window.wView.allowsInlineMediaPlayback = "YES";
    window.wView.mediaPlaybackRequiresUserAction = "NO";
  }
</script>
```   
真实点击必须使用触发 touchend、click、doubleclick 或 keydown 事件等标准的事件才能触发，使用Zepto封装过的tap事件并不能触发播放器的播放
   
2，内联播放（系统会自动接管视频）
```html
<video id="player" webkit-playsinline playsinline > 
```

3，视频中添加交互-即显示dom元素（系统会把视频的层级调到最高，导致dom元素无法显示）   
    
解决方案：   
1.在弹出会显示在视频上方dom的时候暂停视频播放    
2.将视频所在的dom的父元素的高度设为1    
3.处理完弹出的事件后将视频所在的父元素高度还原   

4，去掉默认的播放图标   

```css
video::-webkit-media-controls-start-playback-button {
		display: none;
}
```

5,视频全屏

1，通过webkitRequestFullScreen实现全屏，部分机型需用webkitEnterFullscreen（浏览器接管视频的播放）
```js
var player = $('#player')[0];if (player.webkitSupportsFullscreen) {
    player.webkitEnterFullscreen();
} else {
   player.webkitRequestFullScreen();
}
```

2，伪全屏-样式全屏
	1，点击全屏时，css3旋转实现全屏```css -webkit-transform: rotate(90deg) ```(键盘仍为竖屏模式)
	2，用户在点击全屏时，通过js api来控制webview旋转横屏、



来自：H5 直播避坑指南(https://mp.weixin.qq.com/s/MM5ZwCiWLAeHalsNYMImnw)
