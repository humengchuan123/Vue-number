<template>
	<div class="slide-show" @mouseover="clearRun" @mouseout="run">
		<div class="slide-img">
			<a :href="slides[nowIndex].href" title="">
				<img :src="slides[nowIndex].src" alt="">
			</a>
		</div>
		<h2>{{slides[nowIndex].title}} </h2>
		<ul class="slide-pages">
			<li  class="btn-left" @click="goto(prev)">&lt;</li>
			<li v-for="(item,index) in slides" @click='goto(index)'>
				<a>{{ index + 1 }}</a>
			</li>
			<li  class="btn-right" @click="goto(next)">&gt;</li>
		</ul>
	</div>
</template>

<script>
export default{
	props: {
		slides: {
			type: Array,
			default: []
		},
		inv: {
			type: Number,
			default: 1000
		}
	},
	data () {
		return {
			nowIndex: 0
		}
	},
	computed: {
		prev () {
			if (this.nowIndex === 0) {
				return this.slides.length - 1
			}else {
				return this.nowIndex - 1
			}
		},
		next () {
            if (this.nowIndex === this.slides.length - 1) {
				return 0
			}else {
				return this.nowIndex + 1
			}
		}
	},
	methods: {
		goto (index ) {
			this.nowIndex = index
		},
		run () {
			this.invId = setInterval(() => {this.goto(this.next)},this.inv)
		},
		clearRun () {
			clearInterval(this.invId)
		}

	},
	mounted () {
		this.run()
	}
}
</script>

<style scoped>
.slide-trans-enter-active {
  transition: all .5s;
}
.slide-trans-enter {
  transform: translateX(900px);
}
.slide-trans-old-leave-active {
  transition: all .5s;
  transform: translateX(-900px);
}
.slide-show {
  position: relative;
  margin: 15px 15px 15px 0;
  width: 900px;
  height: 500px;
  overflow: hidden;
}
.slide-show h2 {
  position: absolute;
  width: 100%;
  height: 100%;
  color: #fff;
  background: #000;
  opacity: .5;
  bottom: 0;
  height: 30px;
  text-align: left;
  padding-left: 15px;
}
.slide-img {
  width: 100%;
}
.slide-img img {
  width: 100%;
  position: absolute;
  top: 0;
}
.slide-pages {
  position: absolute;
  bottom: 10px;
  right: 15px;
}
.slide-pages li {
  display: inline-block;
  padding: 0 10px;
  cursor: pointer;
  color: #fff;
}
.slide-pages .btn{
	font-size: 20px;
}
.slide-pages li .on {
  text-decoration: underline;
}	
</style>