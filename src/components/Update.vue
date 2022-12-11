<template>
    <div class="update">
    
    </div>
</template>
<script>
/* eslint-disable */
export default {
    name:'Update',
    mounted() {
        if(localStorage.getItem('authenticated')!="1"){
            this.$router.push('/login');
        }
    },
}
</script>
<style >

</style>