<template>
  <div class="slider">
    <div class="slides">
      <div
        v-for="(slide,index) in slides" 
        :key="index"
        class="slide"
      >
        <div class="slide-image">
          <img
            :src="slide.image.url"
            srcset=""
          >
          <a
            class="live-site-btn"
            :href="slide.link.url"
          >
            <span>{{ slide.link.label }}</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
	export default {
		name: 'Slideshow',
		props: {
			slides: {
				type: Array, 
				default() { 
					return []
				}
			},
 			layout: {
				type: Object, 
				default() {
					return {}
				}
			}
		},
		data: function() {
			return {
				direction: 0,
				location: 0,
				panelWidth: 100,
				panelHeight: 0,
				marginWidth: 6.75,
			};
		},
		computed: {},
		mounted() {},
		methods: {
			moveLeft() {
				this.direction = 0;
				this.location = Math.max(0, this.location - 1) 
			},
			moveRight() {
				this.direction = 1;
				this.location = Math.min(this.projects.length-1, this.location + 1);
			},
		}
	}
</script>

<style lang="scss" scoped>
	@import "@/assets/scss/global-vars.scss";

  .slider{

  }

	.slides{
    // width: 100%;
	}

	.slide{
		// transition-timing-function: ease-in;
		// transition: transform 450ms;
		// transform: translateX(calc(10vw - 0%));
		// margin-right: 5%; 
	}

	.slide-image{
		width: 100%;
		height: 600px;
		background: $highlight;
		position: relative;
	}

	.live-site-btn{
		color: $highlight;
		text-decoration: none; 
		transform-origin: right bottom;
		transform: translate(0.2em, 0px) rotate(90deg);
		position: absolute;
		bottom: 0;
		right:0;
		display: flex;
		overflow: hidden;
		span{
			transition: transform 0.25s 0.4s;
		}
	}

</style>