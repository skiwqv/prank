<template>
    <div class="prank">
        <p v-if="sergey != true" class="timer">{{ formatedTime }}</p>
        <button v-if="sergey != true" class="scary-button" @click="startTimer">ТЫ ГОТОВ?!</button>
        <div class="video-container" v-if="sergey">
            <video class="video" src="../assets/video/Untitled.mp4" type="video/mp4" autoplay loop muted></video>
            <audio loop class="video" autoplay=" true" ref="videoPlayer" :src="sergVIdeo" type="video/mp4" />
        </div>
    </div>
</template>

<script setup>
import sergVIdeo from '@/assets/seraudio.mp3'
const videoPlayer = ref(null)
import { ref, computed } from 'vue';
let counter = ref(5)
let timer = ref(null)
let sergey = ref(false)
let startSergey = ref(false)

let formatedTime = computed(() => {
    const minutes = Math.floor(counter.value / 60);
    const seconds = counter.value % 60;
    return `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
})

function startTimer() {
    startSergey.value = true
    if (startSergey.value == true) {
        timer.value = setInterval(() => {
            if (counter.value > 0) {
                counter.value--
            } else if (counter.value == 0) {
                summonRyazanov()
                clearInterval(timer.value)
            }
        }, 1000)
    }
}

function summonRyazanov() {
    sergey.value = true
}

</script>

<style scoped>
.prank {
    position: absolute;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

}

.timer {
    font-family: 'Creepster', cursive;
    font-size: 24px;
    font-weight: bold;
    color: #8b0000;
    text-shadow: 2px 2px 4px #000;
    letter-spacing: 2px;
    text-transform: uppercase;
    font-size: 62px;
    position: relative;
}



.scary-button {
    font-family: 'Arial', sans-serif;
    position: relative;
    font-size: 18px;
    font-weight: bold;
    padding: 10px 20px;
    border: 2px solid #000;
    background-color: #8b0000;
    color: #fff;
    border-radius: 8px;
    text-transform: uppercase;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.4);
    transition: all 0.3s ease;
}

.scary-button:hover {
    background-color: #ff0000;
    color: #000;
    border: 2px solid #ff0000;
    transform: scale(130%);
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.6);
}

.scary-button::before {
    content: '';
    background-image: url(https://media.discordapp.net/attachments/920258100018184253/1184986673587695647/blood-png-transparent-background-13-700x229.png?ex=658df7d6&is=657b82d6&hm=a9d03ba54d44746567772b29a397d0c10cf6c97a8328ce0af1010388f7b2a608&=&format=webp&quality=lossless&width=875&height=286);
    background-size: cover;
    background-position: center;
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    height: 100px;
    transition: top 0.3s ease;
}


@media (min-width: 770px) {

    .video-container {
        width: 100vw;
        position: relative;
        z-index: 999;
        height: 100vh;
    }

    .video {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        z-index: 999;
        width: 100%;
        height: 100%;
    }
}

@media (max-width: 769px) {

    .video-container {
        width: 100vw;
        background-size: 100%;
        background-position: center;
        position: absolute;
        height: 100vh;
    }

    .video {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        z-index: 999;
        width: 100%;
        height: 100%;
    }
}
</style>