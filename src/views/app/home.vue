<template>
    <div class="page padding">
        <!--问题-->
        <div>
            1、与别人相比，你有什么特殊的学习方法吗？请举例说明。
        </div>
        <div class="mt1rem">
            <textarea name="answer" class="answer" style=""></textarea>
        </div>

        <div class="video-btn mt1rem text-center">
            <input type="file"
                   accept="video/*"
                   capture="camcorder"
                   @change="save"
                   class="video-input">
            <mt-button type="primary" class="recoder-btn">视频录制</mt-button>
        </div>

        <ul v-if="files.length>0">
            <li v-for="(item,index) in files">
                视频{{index+1}}
                &nbsp; &nbsp;
                <i class="fa fa-play" aria-hidden="true" @click="play(item)"></i>
                &nbsp; &nbsp;
                <i class="fa fa-trash" aria-hidden="true" @click="deleteItem(item,index)"></i>
            </li>
        </ul>

        <mt-popup
                v-model="popupVisible"
                closeOnClickModal="true"
                style="width:100%;height:100%"
                position="right">

            <div class="text-center padding">
                <video :src="videoUri" class="video-play" controls></video>
            </div>
            <div class="text-center mt1rem">
                <mt-button type="primary" class="recoder-btn" @click="close">关闭</mt-button>
            </div>
        </mt-popup>

    </div>
</template>
<script>
    export default {
        name: "home",
        data() {
            return {
                files: {},
                popupVisible: false,
                videoUri: ''
            };
        },
        methods: {
            save(event) {
                if (event && event.target && event.target.files) {
                    this.files = event.target.files
                }

            },
            play(item,index) {
                this.popupVisible = true;
                var videoUri = URL.createObjectURL(item);
                this.videoUri = videoUri;
            },
            deleteItem(item,index) {
                this.files = {}
            },
            close() {
                this.popupVisible = false;
                this.videoUri = '';
            }
        }
    };
</script>
<style lang="less" scoped>
    .content {
        padding: 1rem;
        background: #fff
    }

    .answer {
        width: 100%;
        height: 200px;
        border: 1px solid #e4e4e4;
    }

    .video-btn {
        position: relative;
    }

    .video-input {
        position: absolute;
        z-index: 1;
        width: 96px;
        height: 41px;
        opacity: 0;
        top: 0;
        left: 50%;
        margin-left: -48px;
    }

    .recoder-btn {

    }

    .video-play {
        width: 90vw;
        height: 50vw
    }
</style>

