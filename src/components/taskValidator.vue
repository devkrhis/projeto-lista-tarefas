<template>
    <div class="taskValidator">
        <h3> Tarefas </h3>
        <div class="barPercentage">
            <div class="porcentBar" :style="styleWidth"> {{ lengthItems }}%</div>
        </div>
    </div>
    
</template>

<script>
export default {
    props:['listObjects', 'lengthItems'],
    data(){
        return {
            cor: 'green'
        }
    },
    computed: {
        styleWidth(){
            return {
                backgroundColor: this.cor,
                width: this.lengthItems + '%'
            }
        }
    }
    
}
</script>

<style scoped>

.barPercentage {
    border: 3px solid black;
    width: 50%;
    height: 18px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 25%;
}

.porcentBar{
    display: flex;
    justify-content: center;
}



</style>