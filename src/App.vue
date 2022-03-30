<template>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
  <div @keyup.space="action" tabindex="0" >

    <div class="container">
      <div class="result">
        <div>
          choseen tool : {{ choosenTool }}
        </div>
        <div>
          selected mode : {{ mode }}
        </div>
      </div>

      <div class="message">
        <p>
          {{ message }}
        </p>
      </div>
    </div>

    <div class="hand-icon" 
         @click="changeMode"
         :class="{'not-active': handActive}">
      <i class="fas fa-hand-pointer"></i>
    </div>

    <div class="tool-bar">
        <tool-bar
        v-for="tool in toolSet"
        :key="tool.name"
        :item="tool"
        @clickTool="clickTool"
        ></tool-bar>
    </div>

  </div>
  
</template>

<script>
import toolBar from "./components/toolBar.vue"

export default {
  components:{
    toolBar
  },
  data(){
    return{
      toolSet:[
        {
          id:0,
          name:'brush',
          icon:"fas fa-paint-brush",
          selected:false
        },
        {
          id:1,
          name:'magic pen',
          icon:"fas fa-pen",
          selected:false
        },
        {
          id:2,
          name:'eraser',
          icon:"fas fa-eraser",
          selected:false
        },
        {
          id:3,
          name:'pencil',
          icon:"fas fa-pencil-alt",
          selected:false
        },
        {
          id:4,
          name:'pick color',
          icon:"fas fa-crosshairs",
          selected:false
        },
        {
          id:5,
          name:'fill with color',
          icon:"fas fa-fill-drip",
          selected:false
        }
      ],
      mode:'hand',
      choosenTool:'',
      choosenId:null,
      message : 'select tools'
    }
  },
  created(){
    window.addEventListener('keyup', this.keyTool)
    },
  methods:{
    keyTool(event) {
      // console.log(event);
      const shKey = event.key;
      const shId = Number(shKey)-1;
        if(shKey === "Escape"){
          this.changeMode();
        }
        if(this.mode === "keyboard"){
          if(shKey < this.toolSet.length+1){
             this.selectTool(shId);
          }else{
            this.message = 'please select tools by shortkeys';
          }
          return
        }else{
          this.message = 'please change mode, then select tools';
        }
      },
    clickTool(tool){
      if(this.mode === 'hand'){
        this.selectTool(tool.id);
      }else{
        this.message = 'please change mode or select tool by shortkeys';
      }
    },
    selectTool(id){
      this.message = "select tools";
      this.choosenTool = this.toolSet[id].name;
      if(!(this.choosenId === null)){
        this.toolSet[this.choosenId].selected = false;
      }
      this.toolSet[id].selected = true;
      this.choosenId = id;
    },
    changeMode(){
      if(this.mode === 'keyboard'){
            this.mode = 'hand';
            this.message = "mode changed !... now select tool by hand";
          }else{
            this.mode = 'keyboard';
            this.message = "mode changed !... now select tool by shortKeys";
          }
          return
    }
  },
  computed:{
    handActive(){
      return this.mode !== 'hand';
    }
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  text-align: center;
  background-color:#EBD4CB;
}
*::selection{
  color: #DA9F93;
  background-color: #B6465F;
}
.container{
 margin: 2rem auto;
padding: .5rem;
text-align: center;
color: #2C0703;
width: 50%;
box-shadow: 2px 2px 10px #DA9F93;
font-size: 1.1rem;
}
.result{
  display: flex;
  width: 100%;
  padding: 1rem;
}
.result div{
  margin: 0 auto;
}
.message{
  padding: .5rem;
  
}
.message p{
  color: #890620;
  font-weight: bold;
  font-size: 1.4rem;
}
.hand-icon{
  cursor: pointer;
  padding: .2rem;
  color: #890620;
  font-weight: bold;
  font-size: 1.4rem;
  transition: .3s ease-in-out;
}
.hand-icon.not-active,
.hand-icon:hover{
  color: #DA9F93;
}
.tool-bar{
  width:max-content;
  display: flex;
  flex-direction: column;
  margin: .2rem auto;
  padding: 1rem;
  align-items: flex-start;
}

</style>