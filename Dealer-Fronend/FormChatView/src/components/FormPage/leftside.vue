<template>
    <div class="col-4 border bg-light">
        <h6>RECENT CONVERSATION</h6>
            <div
                class="col"
                v-for="(list, index) in array"
                :key="index"
            >
                <div class="row">
                    <div class="col">
                        <b-card >
                            <b-card-text>
                                 <span class="username text-secondary">{{list.userno}}</span>
                                 <span class="time text-secondary">{{list.Time}}</span>
                            </b-card-text>
                            <b-card-text>
                                <span class="text-muted">{{list.Account}}</span>
                            </b-card-text>
                            <span class="text-center">
                            <b-button  variant="outline-primary">Decline</b-button>
                            <b-button v-on:click="selectUser(index)" variant="primary">Accept</b-button>
                            </span>
                        </b-card>
                    </div>
                </div>    
            </div>
    </div>
</template>
<script>
export default {
    name:'Leftside',
    props:['arrayOfUsers'],
    data(){
        
        return{
            array:[
                {userno:'User4',provider:'RV Trader Online',Account:'RV trader Service',Time:'5:03 PM'},
                {userno:'User3',provider:'RV Trader Online',Account:'RV trader Service',Time:'Yesterday'},
                {userno:'User2',provider:'RV Trader Online',Account:'RV trader Service',Time:'Yesterday'},
                {userno:'User1',provider:'RV Trader Online',Account:'RV trader Service',Time:'3/9/21'}
            ]
        }
    },
    methods:{
        selectUser(index){
            this.$emit('UserDetails',this.array[index])
            console.log(this.array[index])
        }
    }
}
</script>
<style>
.header{
    font-size: 15px;
}
.time{
   float: right!important;
}
.username{
    text-align: left;
}
</style>