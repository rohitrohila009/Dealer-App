<template>
    <div class="col-4 border">
        <div v-if="userChatData !== undefined">
            <div class="row">
                <div class="col">
                <b-card >
                    <b-card-text>
                        <span class="text-secondary">{{userChatData.userno}}</span>
                        <span class="text-secondary time">{{userChatData.Time}}</span><br>
                        <span style="font-size: 10px;" class="text-muted">Provider {{userChatData.provider}}</span>
                    </b-card-text>
                </b-card>   
                </div> 
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name:'MiddlePart',
    props:['userChatData']
}
</script>
<style>
.time{
    float: right;
}
</style>