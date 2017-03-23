<template>
  <div id="app" @click.stop.prevent = "specialClick">
  	<div class="coverTit">
	    <ul class="choose">
	      <li @click.stop.prevent = "handelClick(null,index)" 
	      		class="normalStyle normalStyleTouch" 
	      		v-for = "(main,index) in titles"
	      		ref = "sign"
	      		:class = "{clicked:isMainClick[index]}">{{main.title}}</li>
	    </ul>
	    <ul v-on:show = "appear"
	    		v-on:disappert = "hidden"
	    	 	v-show = "isShowSecondTitles"
	      	class="secTitNormal">
	      <li v-for = "(sec,index) in titleHiddens"
	      		@click.stop.prevent = "secClick(null,index)"
	      		class="secTitChild"
	      		:class = "{secClicked:isclick[index],secNormalStyle:isSec[index]}">{{sec.title}}</li>
	    </ul>
    </div>
    <div class="content">
    	<div v-show = "firstMsg">
	    	<p v-for = "(mainC,index) in contents"
	    		 v-on:remove = "change"
	    		 v-show = "isShowList[index]">{{mainC.content}}</p>
	    </div>
	    <div v-show = "secMsg">
	    	<p v-for = "(secContent,index) in secContents"
	    		 v-show = "isShowSec[index]"
	    		 v-on:secShow = "secChange">{{secContent.content}}</p>
	    </div>
	   </div>
  </div>
</template>

<script>
const titles = [{title:'Home',},{title:'Profile'},{title:'Dropdown'}]
const titleHiddens = [{title:'@fat'},{title:'@mdo'}]
const contents = [{content:"Raw denim you probably haven't heard of them jean shorts Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro keffiyeh dreamcatcher synth. Cosby sweater eu banh mi, qui irure terry richardson ex squid. Aliquip placeat salvia cillum iphone. Seitan aliquip quis cardigan american apparel, butcher voluptate nisi qui."},{content:"Food truck fixie locavore, accusamus mcsweeney's marfa nulla single-origin coffee squid. Exercitation +1 labore velit, blog sartorial PBR leggings next level wes anderson artisan four loko farm-to-table craft beer twee. Qui photo booth letterpress, commodo enim craft beer mlkshk aliquip jean shorts ullamco ad vinyl cillum PBR. Homo nostrud organic, assumenda labore aesthetic magna delectus mollit. Keytar helvetica VHS salvia yr, vero magna velit sapiente labore stumptown. Vegan fanny pack odio cillum wes anderson 8-bit, sustainable jean shorts beard ut DIY ethical culpa terry richardson biodiesel. Art party scenester stumptown, tumblr butcher vero sint qui sapiente accusamus tattooed echo park."}]
const secContents = [{content:"ProfileDropdownTrust fund seitan letterpress, keytar raw denim keffiyeh etsy art party before they sold out master cleanse gluten-free squid scenester freegan cosby sweater. Fanny pack portland seitan DIY, art party locavore wolf cliche high life echo park Austin. Cred vinyl keffiyeh DIY salvia PBR, banh mi before they sold out farm-to-table VHS viral locavore cosby sweater. Lomo wolf viral, mustache readymade thundercats keffiyeh craft beer marfa ethical. Wolf salvia freegan, sartorial keffiyeh echo park vegan"},{content:"Etsy mixtape wayfarers, ethical wes anderson tofu before they sold out mcsweeney's organic lomo retro fanny pack lo-fi farm-to-table readymade. Messenger bag gentrify pitchfork tattooed craft beer, iphone skateboard locavore carles etsy salvia banksy hoodie helvetica. DIY synth PBR banksy irony. Leggings gentrify squid 8-bit cred pitchfork. Williamsburg banh mi whatever gluten-free, carles pitchfork biodiesel fixie etsy retro mlkshk vice blog. Scenester cred you probably haven't heard of them, vinyl craft beer blog stumptown. Pitchfork sustainable tofu synth chambray yr."}]
export default {
  name: 'app',
  data () {
    return {
      titles,
      titleHiddens,
      contents,
      secContents,
      isShowList:[true,false],
      isShowSecondTitles:false,
      isclick:[false,false],
      isSec:[true,true],
      isShowSec:[false,false],
      isMainClick:	[true,false,false],
      firstMsg:true,
      secMsg:false
    }
  },
  methods:{
  	handelClick(e,index){
  		if(this.isShowList[index] === true){
  			return false
  		}else{
	  		this.isShowList[index]=this.change(index)			
  			this.$refs.sign[index].classList.remove('normalStyleTouch')
  		}
//		alert('be clicked',this.isShowList[index])
  		if(index === 2){
  			if(this.isShowSecondTitles ===	true){
  				console.log('i would be false')
  				this.hidden()
  			}else{
					this.appear() 				
  			}
				this.isMainClick[index] = false
  		}else if(index < 2){
  			this.firstMsg = true
  			this.secMsg = false
				this.hidden()
  		}
			const list = [false,false,false]
			this.isMainClick[index] = !this.isMainClick[index]
			list[index] = this.isMainClick[index]
			this.isMainClick = Object.assign([],list)
  	},
  	change(index){
			const list = [false,false]
			if(index<2){
				this.isShowList[index] = !this.isShowList[index]
				list[index] = this.isShowList[index]
				this.isShowList = Object.assign([],list)
//				alert('i would be changed')
			}else{
				return false
			}
  	},
  	appear(){
  		this.isShowSecondTitles = true
  	},
  	hidden(){
  		this.isShowSecondTitles = false
  	},
  	secClick(e,index){
  		if(index >= 0){
  			this.firstMsg = false
  			this.secMsg = true
  		}
			const list = [false,false]
			const sec = [true,true]
		if(this.isclick[index] === true){
  		this.hidden()
			return false
		}else{
  		this.isclick[index] = !this.isclick[index]
		}
  		this.isSec[index] = !this.isSec[index]			
  		sec[index] = this.isSec[index]
  		this.isSec = Object.assign([],sec)
  		list[index] = this.isclick[index]
  		this.isclick = Object.assign([],list)
  		this.secChange(index)
  		this.hidden()
  	},
  	secChange(index){
  		const list = [false,false]
  		this.isShowSec[index] = !this.isShowSec[index]
  		list[index] = this.isShowSec[index]
  		this.isShowSec = Object.assign([],list)
  	},
  	specialClick(){
		if(this.isShowSecondTitles === true){	
				this.isShowSecondTitles = false
		}else{
			return false   
		}
  	}
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
  border: 1px solid lightgray;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
p{text-indent: 2rem;}
.coverTit{position: relative;}
.choose{overflow: hidden;margin-left: 10px;}
.normalStyle{float: left;color: mediumpurple;cursor: pointer;padding: 5px 10px;transition: all .5s;border-bottom: 1px dashed lightgray;}
.normalStyle.clicked{border: 1px dashed lightgray;border-bottom: 1px dashed transparent;}
.normalStyleTouch:hover{color:deepskyblue;background-color: lightgrey;}
.secNormalStyle:hover{background-color: darkgray;}
.secClicked{background-color: cornflowerblue; color: white;}
.secTitNormal{background-color: white;position: absolute;left: 140px;top: 15px;}
.secTitChild{padding: 2px 23px;}
</style>
