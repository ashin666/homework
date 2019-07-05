<template>
    <div>
        <div>请点击我一下</div>
    </div>
</template>
<script>
    export default {
        name:"child",
        methods:{
            childclick(e){
                console.log(e)
            }
        }
    }
</script>
