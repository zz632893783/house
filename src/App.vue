<template>
    <div id="container" ref="container"></div>
</template>
<script setup>
import { ref, onMounted } from 'vue';
import AMapLoader from '@amap/amap-jsapi-loader';

const container = ref();

let map;

const initAMap = async () => {
    window._AMapSecurityConfig = { securityJsCode: 'fc838dc14ec09d7c33fd592e2d10355a' };

    const AMap = await AMapLoader.load({
        key: 'a3b9dfc352a06c921a1c0f83800d5e76',
        version: '2.0',
        plugins: ['AMap.Scale', 'AMap.Marker']
    });

    map = new AMap.Map(container.value, {
        viewMode: '3D',
        zoom: 11,
        center: [120.197212, 30.280398]
    });
    const houseList = [
        {
            name: '星缦云渚城',
            center: [120.093475, 30.359159],
            houseType: '3室',
            area: '99',
            price: '250-260',
            metroDistance: '1公里',
            carPark: false
        },
        {
            name: '锦上云澜',
            center: [120.32786, 30.326548],
            houseType: '3室',
            area: '99',
            price: '270',
            metroDistance: '2公里',
            carPark: true
        },
        {
            name: '潮映望月',
            center: [120.330725,30.324544],
            houseType: '3室',
            area: '99',
            price: '280',
            metroDistance: '2公里',
            carPark: false
        },
        {
            name: '拾光翠语',
            center: [120.253081,30.115664],
            houseType: '3室',
            area: '95-103',
            price: '230-280',
            metroDistance: '500米',
            carPark: false
        },
        {
            name: '棠前明月',
            center: [120.29979,30.188775],
            houseType: '3室',
            area: '95-106',
            price: '240-300',
            metroDistance: '2.3公里',
            carPark: false
        },
        {
            name: '璞御栖湖府',
            center: [120.079915,30.111665],
            houseType: '3室',
            area: '110',
            price: '280-310',
            metroDistance: '700米',
            carPark: false
        },
        {
            name: '听翠轩',
            center: [120.111052,30.34459],
            houseType: '3室',
            area: '97',
            price: '276最低',
            metroDistance: '2.1公里',
            carPark: false
        },
        {
            name: '璀璨映澜',
            center: [120.295863,30.356799],
            houseType: '3室',
            area: '99',
            price: '260-270',
            metroDistance: '1.2公里',
            carPark: true
        },
        {
            name: '潮阅尚境',
            center: [120.30549,30.366447],
            houseType: '3室/4室',
            area: '98-125',
            price: '210-300',
            metroDistance: '1.3公里',
            carPark: true
        }
    ];

    houseList.forEach(n => {
        const marker = new AMap.Marker({
            position: n.center,
            offset: new AMap.Pixel(0, 0),
            content: ``
        })
        const markerContent = document.createElement('div');
        marker.setPosition(n.center);
        markerContent.innerHTML = `
            <div class="root">
                <i class="circle"></i>
                <i class="dot"></i>
                <div class="house">
                    <h4 class="name">${ n.name }</h4>
                    <label class="label">面积</label>
                    <span class="content">${ n.area }㎡</span><br/>
                    <label class="label">总价</label>
                    <span class="content">${ n.price }</span><br/>
                    <label class="label">地铁距离</label>
                    <span class="content">${ n.metroDistance }</span><br/>
                    <label class="label">是否送车位</label>
                    <span class="content">${ n.carPark ? '是' : '否' }</span>
                </div>
            </div>
        `
        marker.setContent(markerContent);
        marker.setMap(map);
    });
    // const overlay = new AMap.LabelOverlay({
    //     content: div,
    //     offset: new AMap.Pixel(10, -30)
    // });


    // map.add(overlay);
};

onMounted(initAMap);
</script>
<style lang="scss" scoped>
#container {
    border: 1px solid red;
    width: 100vw;
    height: 100vh;
}
:deep(.root) {
    border: 1px solid red;
    position: relative;
    .circle {
        position: absolute;
        width: 12px;
        height: 12px;
        border: 1px solid red;
        border-radius: 50%;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
    .dot {
        border-top: 8px solid white;
        border-right: 6px solid transparent;
        border-left: 6px solid transparent;
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translate(-50%, 0);
        filter: drop-shadow(1px 1px 0 black) drop-shadow(-1px 1px 0 black);
        z-index: 1;
    }
    .house {
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translate(-50%, -7px);
        white-space: nowrap;
        padding: 6px;
        background: white;
        filter: drop-shadow(1px 1px 0 black) drop-shadow(-1px -1px 0 black);
        .name {
            font-size: 14px;
        }
        .label {
            font-size: 12px;
        }
        .content {
            font-size: 12px;
        }
    }
}
</style>