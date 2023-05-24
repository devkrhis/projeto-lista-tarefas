<template>
    <div class="newTasks">
        <TaskValidator class="distance" :listObjects="arrayListObject" :lengthItems="totalItens"/>

        <input v-model="taskName" @keyup.enter="addNewItem" type="text"> 
        <li class="itemBox" v-for="(item, index) in arrayListObject" :key="index.tarefa"
        :class="changeColorGreen(index)"
        @click="mouseEvent(index)"
        >
            {{ item.taskName }}
            <button type="button" @click.stop="removeItem(item)"> X </button>
        </li>
    </div>
    
</template>

<script>
import TaskValidator from './taskValidator.vue';
export default {
    components: {
        TaskValidator
    },
    data(){
        return {
            filterItens: {},
            quantItens: 0,
            totalItens: 0,
            taskName: '',
            idSelected: -1,
            arrayListObject: [
            ],
        }
    },
    methods: {
        addNewItem(){
            let newItemThisObject = {
                taskName: this.taskName,
                valueItem: false
            }
            this.arrayListObject.push(newItemThisObject)
            this.taskName = ''
            console.log("this.arrayListObject", this.arrayListObject)
            this.quantItens = this.arrayListObject.length
            console.log('this.quantItens', this.quantItens)

            this.filterItens = this.arrayListObject.filter((returnCondition) => {
                if(returnCondition.valueItem === true){
                    return returnCondition.valueItem
                }
            })
            console.log('this.filterItens top', this.filterItens.length)

            if(this.arrayListObject.length > 0){
                return this.totalItens = (this.filterItens.length*100) / this.quantItens 
            }
            
            console.log('this.quantItens', this.totalItens)

            
        
        },
        removeItem(item){
            const index = this.arrayListObject.indexOf(item);
            if(index > -1){
                this.arrayListObject.splice(index ,1)

                this.quantItens = this.arrayListObject.length
                this.filterItens = this.arrayListObject.filter((returnCondition) => {
                if(returnCondition.valueItem === true){
                    return returnCondition.valueItem
                }
                })
            console.log('this.filterItens top', this.filterItens.length)

            if(this.arrayListObject.length > 0){
                return this.totalItens = (this.filterItens.length*100) / this.quantItens 
            }
            else if(this.arrayListObject.length == 0){
                return this.totalItens = 0
            }
            }





        },
        mouseEvent(event){
            if(this.arrayListObject[event].valueItem == false){
                this.arrayListObject[event].valueItem = true
                this.idSelected = event
            } else {
                this.arrayListObject[event].valueItem = false
                this.idSelected = event
            }

            this.filterItens = this.arrayListObject.filter((returnCondition) => {
                if(returnCondition.valueItem === true){
                    return returnCondition.valueItem
                }
            })
            console.log('this.filterItens top', this.filterItens.length)

            if(this.arrayListObject.length > 0){
                return this.totalItens = (this.filterItens.length*100) / this.quantItens 
            }
            
            console.log('this.quantItens', this.totalItens)

        },
        changeColorGreen(event){
            return {
                estiloGreen: this.arrayListObject[event].valueItem

            }
        }
    },
    
}
</script>

<style scoped>

.itemBox {
    border: 1px solid black;
    margin-left: 500px;
    margin-right: 500px;
    margin-bottom: 10px;
    background-color: red;
    
}

.newTasks input {
    margin-bottom: 15px;
}

.estiloGreen {
    background-color: green;
}

.distance {
    margin-bottom: 50px;
}


</style>