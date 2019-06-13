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
        
var audios = document.getElementsByTagName("audio");
// 暂停函数
function pauseAll() {
    var self = this;
    [].forEach.call(audios, function (i) {
        // 将audios中其他的audio全部暂停
        i !== self && i.pause();
    })
}
// 给play事件绑定暂停函数
[].forEach.call(audios, function (i) {
    i.addEventListener("play", pauseAll.bind(i));
    
    // 音频和视频互斥 
         handleAV(tag) {

            let tags = document.getElementsByTagName(tag);

            for (let i = tags.length - 1; i >= 0; i--) {
                 (function(){
                    let p = i;
                    tags[p].addEventListener('play',function(){
                        pauseAll(p);
                    })
                })()
            }

            function pauseAll(index) {
                for (let j = tags.length - 1; j >= 0; j--) {
                    if (j!=index) {
                        tags[j].pause();
                    }    
                }
                if (tag === 'audio'){
                    pauseOther('video')
                }
                if (tag === 'video') {
                    pauseOther('audio')
                }
            }
            function pauseOther(type) {
                let types = document.getElementsByTagName(type);
                for (let k = types.length - 1; k >= 0; k--) {
                    types[k].pause()
                }
            }
        },   
  
```
