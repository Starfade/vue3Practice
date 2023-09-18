<template>
    <div>
        <div class="gamestatus">
            <h2>得分:{{ score }}</h2>
            <h2>等级:{{ level == 9 ? 'max' : level }}</h2>
            <h2>生命:{{ live }}</h2>
        </div>
        <div class="gamearea">
            <div class="start" v-if="status == 0" @click="gameStart">游戏开始</div>
            <div v-for="(e, i) in pots" :style="{
                top: e.top,
                left: e.left,
                height: e.size,
                width: e.size,
                transform: `rotate(${e.rotate})`,
                pointerEvents: e.canclick,
            }" :class="{ dead: e.canclick == 'none' }" class="pot" @click="addScore(i, e)"></div>
            <div v-if="status == 2" class="gameover" @click="gameStart">
                <h2>游戏结束</h2>
                <p>您获得了{{ score }}分</p>
            </div>
        </div>
    </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
const score = ref(0)
const live = ref(0)
const status = ref(0)
const level = ref(0)
let time = 0
let temptime = 0
let timeset: any
let candown = false
interface pot {
    top: string,
    left: string,
    size: string,
    rotate: string,
    canclick: any,
    timer:any
}
const temp: pot[] = [];
const pots = ref(temp)
function addScore(i: number, e: any) {
    live.value++
    score.value++
    e.canclick = ref('none')
    e.timer=setTimeout(() => {
        pots.value.splice(i, 1)
    }, 50);
    candown = true
}
function gameStart() {
    status.value = 1
    live.value = 5
    time = 10
    level.value = 0
    candown = false
    score.value = 0
    timeset = setInterval(() => {
        temptime++
        // console.log(temptime,time)
        if (temptime >= time) {
            temptime = 0
            let pot = {
                top: (Math.random() * 95) + '%',
                left: (Math.random() * 95) + '%',
                size: (30 + Math.random() * 50) + 'px',
                rotate: (Math.random() * 360) + 'deg',
                canclick: ref('all'),
                timer:null,
            }
            pots.value.push(pot)
            live.value--
            if (live.value <= 0) {
                clearInterval(timeset)
                pots.value = []
                status.value = 2
            }
        }
        if (candown && score.value % 20 == 0 && time > 1) {
            level.value++
            time--
            candown = false
        }
    }, 100)
}
</script>
<style lang="less">
.gamestatus {
    display: flex;
    justify-content: space-around;
}

.gamearea {
    position: relative;
    overflow: hidden;
    width: 100vw;
    height: 93vh;

    .start {
        top: calc(50% - 50px);
        left: calc(50% - 50px);
        height: 100px;
        width: 100px;
        border-radius: 50%;
        background-color: lightgray;
        text-align: center;
        line-height: 100px;
        position: absolute;
    }

    .pot {
        top: 50%;
        left: 50%;
        background-size: cover;
        position: absolute;
        animation: potin 0.2s;
        background-image: url(../assets/漏洞.png);
    }

    .dead {
        background-image: url(../assets/漏洞dead.png);
    }

    @keyframes potin {
        from {
            transform: scale(0);
        }

        to {
            transform: scale(1);
        }
    }

    .gameover {
        background-color: white;
        box-shadow: 0 0 5px 5px lightgray;
        text-align: center;
        padding: 20px;
        border-radius: 10px;
        position: absolute;
        height: 100px;
        width: 200px;
        margin: auto;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
    }
}
</style>