# note
日常笔记
### h5页面多个音频仅仅播放一个
```
        var videos = document.getElementsByTagName('video');
            for (var i = videos.length - 1; i >= 0; i--) {
                (function(){
                    var p = i;
                    videos[p].addEventListener('play',function(){
                        pauseAll(p);
                    })
                })()
            }
            function pauseAll(index){
                for (var j = videos.length - 1; j >= 0; j--) {
                    if (j!=index) videos[j].pause();
                }
            };
```
