<template>
    <div id="container">
        <div id="main" @mousedown.capture="move">
            <div id="app">       <!--绑定按下事件-->
            </div>
        </div>
        <div id="test" @mousedown="move">

        </div>
    </div>
</template>

<script>
    function showInfoDragstart(e, event) {
        var text = '开始拖拽地图！'
        console.log(text);
    }

    function showInfoDragging(e) {
        var text = '正在拖拽地图！'

        let odiv = document.getElementById('app');        //获取目标元素
        console.log(odiv);

        //算出鼠标相对元素的位置
        let disX = e.clientX - odiv.offsetLeft;
        let disY = e.clientY - odiv.offsetTop;
        document.onmousemove = (e) => {       //鼠标按下并移动的事件
            //用鼠标的位置减去鼠标相对元素的位置，得到元素的位置
            let left = e.clientX - disX;
            let top = e.clientY - disY;

            //绑定元素位置到positionX和positionY上面
            this.positionX = top;
            this.positionY = left;

            //移动当前元素
            odiv.style.left = left + 'px';
            odiv.style.top = top + 'px';
        };
        document.onmouseup = (e) => {
            document.onmousemove = null;
            document.onmouseup = null;
        };
    }

    function showInfoDragend() {
        var text = '拖拽地图结束！'
    }

    export default {
        name: 'app',
        data() {
            return {
                positionX: 0,
                positionY: 0,
            }
        },
        created() {
            var mapOpts = {
                showIndoorMap: false, // 是否在有矢量底图的时候自动展示室内地图，PC默认true,移动端默认false
                resizeEnable: true, //是否监控地图容器尺寸变化，默认值为false
                dragEnable: true, // 地图是否可通过鼠标拖拽平移，默认为true
                keyboardEnable: false, //地图是否可通过键盘控制，默认为true
                doubleClickZoom: false, // 地图是否可通过双击鼠标放大地图，默认为true
                zoomEnable: false, //地图是否可缩放，默认值为true
                rotateEnable: false, // 地图是否可旋转，3D视图默认为true，2D视图默认false
            }
            window.onLoad = function () {
                var map = new AMap.Map('app', mapOpts);
                // map.event.removeListener(clickListener);
                // map.on('dragstart', showInfoDragstart);
                // map.on('dragging', showInfoDragging);
                // map.on('dragend', showInfoDragend);

                AMap.event.addListener(map, "mousedown", function (e) {
                });
                AMap.event.addListener(map, "mousemove", function (e) {
                });
                // AMap.event.addListener(map, "dragging", function(e) {
                //     console.log(e);
                // });
                // AMap.event.addListener(map, "dragend", function(e) {
                //     console.log(e);
                // });
            }
            var url = 'https://webapi.amap.com/maps?v=1.4.15&key=您申请的key值&callback=onLoad';
            var jsapi = document.createElement('script');
            jsapi.charset = 'utf-8';
            jsapi.src = url;
            document.head.appendChild(jsapi);
        },
        mounted() {
            // var map = new AMap.Map('app', {
            //   zoom:11,//级别
            //   center: [116.397428, 39.90923],//中心点坐标
            //   viewMode:'3D'//使用3D视图
            // });
        },
        methods: {
            move(e) {
                let odiv = document.getElementById('main');        //获取目标元素
                console.log(e);
                console.log(odiv);

                //算出鼠标相对元素的位置
                let disX = e.clientX - odiv.offsetLeft;
                let disY = e.clientY - odiv.offsetTop;
                document.onmousemove = (e) => {       //鼠标按下并移动的事件
                    //用鼠标的位置减去鼠标相对元素的位置，得到元素的位置
                    let left = e.clientX - disX;
                    let top = e.clientY - disY;

                    //绑定元素位置到positionX和positionY上面
                    this.positionX = top;
                    this.positionY = left;

                    //移动当前元素
                    odiv.style.left = left + 'px';
                    odiv.style.top = top + 'px';
                };
                document.onmouseup = (e) => {
                    document.onmousemove = null;
                    document.onmouseup = null;
                };
            },

        },
    }
</script>

<style>
    #container {
        position: relative;
        height: 100vh;
        width: 100vw;
    }

    #app {
        /*position: absolute; !*定位*!*/
        display: inline-block;
        /*top: 10px;*/
        /*left: 10px;*/
        width: 300px;
        height: 600px;
        background: #666; /*设置一下背景*/
    }

    #test {
        position: absolute; /*定位*/
        display: inline-block;
        top: 100px;
        left: 100px;
        width: 300px;
        height: 600px;
        background: #666; /*设置一下背景*/
    }
    #main {
        overflow: hidden;
        position: relative;
        display: inline-block;
        padding: 0;
    }
</style>
