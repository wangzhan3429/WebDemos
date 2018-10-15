<template>
	<div>
		<div id="container" @mouseover='stop()' @mouseout="play()">
			<div id="list" style="left: -200px;" ref='list'>
				<img src="../../build/default.png" alt="1" />
				<img src="../../build/logo.png" alt="1" />
				<img src="../../build/default.png" alt="2" />
				<img src="../../build/logo.png" alt="3" />
				<img src="../../build/default.png" alt="4" />
				<img src="../../build/logo.png" alt="5" />
			</div>

			<div id="buttons" ref='buttons'>
				<span index="1" class="on"></span>
				<span index="2"></span>
				<span index="3"></span>
				<span index="4"></span>
				<span index="5"></span>
			</div>
			<a href="javasrcipt:;" id="prev" class="arrow" ref='prev' @click="prev()">&lt;</a>
			<a href="javasrcipt:;" id="next" class="arrow" ref='next' @click="next()">&gt;</a>
		</div>

	</div>

</template>

<script>
	export default {
		data() {
			return {
				index: 1,
				timer:Object,
			}
		},
		mounted: function() {
			const self = this;
			this.play()
			// self.$refs.container.onmouseover = stop;
			// self.$refs.container.onmouseout = play;
			console.log('---'+self.$refs.buttons.children[0].attributes['index'].value);
			for(var i = 0;i<self.$refs.buttons.children.length;i++){
				(function(i){
					self.$refs.buttons.children[i].onclick=function(){
						var clickIndex = parseInt(self.$refs.buttons.children[i].attributes['index'].value);
						var offset = 200*(self.index - clickIndex);
						self.animate(offset);
						self.index = clickIndex;
						self.buttonShow()
						
					}
				})(i)
				
			}
			
		},
		methods: {
			play: function() { //重复执行的定时器,,
			console.log('----play');
				const self = this;
				self.timer = setInterval(function() {
					self.next()
					//	next.onclick();
				}, 2000)

			},
			prev: function() {
				this.index--;
				if (index < 1) {
					index = 5
				}
				this.buttonShow();
				this.animate(200)
			},
			next: function() {
				this.index++;
				if (this.index > 5) {
					this.index = 1
				}
				this.buttonShow();
				this.animate(-200)
			},
			buttonShow: function() {
				const self = this;
				console.log('---' + self.$refs.buttons.children.length);
				for (var i = 0; i < self.$refs.buttons.children.length; i++) {
					if (self.$refs.buttons.children[i].className == 'on') {
						self.$refs.buttons.children[i].className = '';
					}
				}
				console.log('==='+self.index);
				self.$refs.buttons.children[self.index - 1].className = 'on';
			},
			stop: function() {
				console.log('----stop');
				var self = this;
				clearInterval(self.timer);
			},
			animate:function(offset){
				var self = this;
				var newLeft = parseInt(self.$refs.list.style.left)+offset;
				self.$refs.list.style.left = newLeft+"px"
				if(newLeft > -200){
					self.$refs.list.style.left=-1000+"px"
				}
				if(newLeft < -1000){
					self.$refs.list.style.left=-200+"px"
				}
			}


		}


	}
</script>

<style>
	#container {
		position: relative;
		width: 200px;
		height: 200px;
		overflow: hidden;
		align-content: center;
	}

	#container:hover .arrow {
		display: block;
	}

	#list {
		position: absolute;
		z-index: 1;
		width: 1600px;
		height: 200px;
	}

	#list img {
		float: left;
		width: 200px;
		height: 200px;
	}

	#buttons {
		position: absolute;
		left: 50px;
		z-index: 2;
		height: 10px;
		bottom: 20px;

	}

	#buttons .on {
		background: orangered;
	}

	#buttons span {
		float: left;
		margin-right: 5px;
		height: 10px;
		width: 10px;
		border: 1px solid #FFFFFF;
		border-radius: 50%;
		background: #333;
		cursor: pointer;
	}

	.arrow {
		position: absolute;
		top: 80px;
		z-index: 2;
		width: 40px;
		height: 40px;
		cursor: pointer;
		text-align: center;
		line-height: 39px;

	}

	.arrow:hover {
		background-color: RGBA(0, 0, 0, .7);
	}

	#prev {
		left: 20px;
	}

	#next {
		right: 20px;
	}
</style>

<!-- .styl  文件是啥？？ -->
