<script setup lang="js">
import TRTCCloud, {TRTCAppScene, TRTCParams} from 'trtc-electron-sdk';

const trtc = new TRTCCloud();


//本人进入房间回调
function onEnterRoom(elapsed) {
    console.log(`onEnterRoom: elapsed: ${elapsed}`);
}

//本人离开房间回调
function onExitRoom(reason) {
    console.log(`onExitRoom: reason: ${reason}`);
}

//房间错误回调
function onError(errCode, errMsg) {
    console.log(`onError: errCode: ${errCode}, errMsg: ${errMsg}`);
}

//房间警告回调
function onWarning(warningCode, warningMsg) {
    console.log('onwarning', warningCode, warningMsg);
}

// 远端用户进入房间回调
function onRemoteUserEnterRoom(userID) {
    console.log(userID);
}

//远端用户离开房间回调
function onRemoteUserLeaveRoom(userID, reason) {
    console.log(userID, reason);
}

// 远端开关视频回调
function onUserVideoAvailable(userID, available) {
    console.log(userID, available);
}

// 远端开关麦克风回调
function onUserAudioAvailable(userID, available) {
    console.log(userID, available);
}

// 房间声音回调
function onUserVoiceVolume(userVolumes, userVolumesCount, totalVolume) {
    console.log(userVolumes, userVolumesCount, totalVolume);
}

const initMeetingCallback = () => {
    trtc.on('onError', onError);
    trtc.on('onEnterRoom', onEnterRoom);
    trtc.on('onExitRoom', onExitRoom);
    trtc.on('onWarning', onWarning);
    trtc.on('onRemoteUserEnterRoom', onRemoteUserEnterRoom);
    trtc.on('onRemoteUserLeaveRoom', onRemoteUserLeaveRoom);
    trtc.on('onUserVideoAvailable', onUserVideoAvailable);
    trtc.on('onUserAudioAvailable', onUserAudioAvailable);
    trtc.on('onUserVoiceVolume', onUserVoiceVolume);
};
const login = () => {
    initMeetingCallback();
    enterMeetingRoom();
};

const enterMeetingRoom = () => {
    //todo测试数据替换{meetingHeader.meetingID,userID:userInfo.userId,userName:userInfo.userName}
    const trtcParams = new TRTCParams();
    trtcParams.userId = 'denny';
    trtcParams.sdkAppId = 1600000376;
    trtcParams.userSig = 'eJyrVgrxCdYrSy1SslIy0jNQ0gHzM1NS80oy0zLBwkB2XiVUojglO7GgIDNFycrQzAAEjM3NIDKpFQWZRalAcVNTUyOgBES0JDMXJGZmaWhsaWpsZg41JTMdaK5JSaZhvnaop0Ghc4y*R2pAZY55YEluUbZJeW56qnekn2GGt3*GgWWeq2dWsa1SLQBfBjHk';
    trtcParams.roomId = 20230809;
    trtc.enterRoom(trtcParams, TRTCAppScene.TRTCAppSceneVideoCall);
}
</script>

<template>
    <h1>{{ msg }}</h1>
    <div class="card">
        <button type="button" @click="login">login</button>
        <p>
            Edit
            <code>components/HelloWorld.vue</code> to test HMR
        </p>
    </div>
    
    <p>
        Check out
        <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
        >create-vue</a
        >, the official Vue + Vite starter
    </p>
    <p>
        Install
        <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
        in your IDE for a better DX
    </p>
    <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
    color: #888;
}
</style>
