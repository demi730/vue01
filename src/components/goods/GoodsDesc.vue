<template>
    <div class="goodsdesc-container">
        <h3>{{info.title}}</h3>
        <div class="content" v-html="info.content"></div>
    </div>
</template>
<script>
    import {Toast} from 'mint-ui'
    export default{
        data(){
            return {
                id:this.$route.params.id,
                info:{}
            }
        },
        created(){
            this.getGoodsDesc()
        },
        methods:{
            getGoodsDesc(){
                this.$http.get('api/goods/getdesc/'+this.id).then(result=>{
                    if (result.body.status===0){
                        this.info = result.body.message[0]
                    }else{
                        Toast('数据加载失败！')
                    }
                })
            }
        }
    }
</script>

<style lang="scss">
    .goodsdesc-container{
        padding: 4px;
        h3{
            font-size: 16px;
            color: #226aff;
            margin: 15px 0;
            text-align: center;
            .content{
                img{
                    width: 100%;
                }
            }
        }
    }
</style>