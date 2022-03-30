<template>

    <div class="item">
        <div @click="$emit('clickTool',Item)"
        @mousemove="$emit('clickTool',Item)"
        :class="{'select-item' : Item.selected }">
            <i :class="Item.icon"></i>
            <!-- <span>{{ Item.name }} </span> -->
        </div>
    </div> 

</template>

<script>
export default {
    props:[
        'item'
    ],
    emits:[
        'clickTool'
    ],
    data(){
        return{
            Item:this.item
        }
    },
    computed:{
        selectedOrNot(tmp){
            return tmp.selected ? 'select-item' : ''
        } 
    }

}
</script>

<style scoped>
.item{
    margin: .5rem;
    padding: 0 .5rem;
    cursor: pointer;
    transition: .5s ease-in-out;
    color: #890620;
    border-left: 3px solid transparent;
    border-right: 3px solid transparent ;
    font-weight: bolder;
}
.item:hover,
.select-item{
    color: #B6465F;
    border-color: #DA9F93;
}


</style>