<template>
  <div
    class="project-carousel"
    :style="setHeight"
  >
    <nav class="arrows">
      <div
        class="left arrow" 
        :class="leftArrowClass"
        @click="moveLeft"
      />
      <div
        class="right arrow" 
        :class="rightArrowClass"
        @click="moveRight"
      />
    </nav>
    <div
      ref="carouselProjects"
      class="projects"
      :class="numOfPanels"
    >
      <div
        v-for="(project,index) in projects" 
        :key="index"
        class="project"
        :style="offset(index)"
        :class="saturate(index)"
      >
        <div class="project-description">
          <h4 class="project-title">
            <span>{{ project.company }}</span>
          </h4>
          <p class="project-summary">
            {{ project.summary }}
          </p>
        </div>
        <div class="project-image">
          <img
            :src="project.image.url"
            srcset=""
          >
          <a
            class="view-code-btn"
            :href="project.codeURL"
          >
            <span>view-code</span>
          </a>
          <a
            class="live-site-btn"
            :href="project.link.url"
          >
            <span>{{ project.link.label }}</span>
          </a>
        </div>
				
        <div class="overlay" />
      </div>
    </div>
  </div>
</template>

<script>
	export default {
		name: 'Carousel',
		props: {
			projects: {
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
				panelsDisplayed: 2,
			};
		},
		computed: {
			leftArrowClass(){
				return {
					active : (this.location > 0) && (this.location < this.projects.length)
				}
			},
			rightArrowClass(){
				return {
					active : (this.location >= 0) && (this.location < this.projects.length-1)
				}
			},
			numOfPanels(){
				switch (this.panelsDisplayed) {
					case 1: 
						return "one-panel";
					case 2:
						return "two-panel";
					case 3:
						return "three-panel";
					default:
						return "one-panel";
				}
			},
			setHeight(){
				return `height: ${this.panelHeight * 0.65}px;`;
			},
		},
		mounted() {
			this.calcHeight();
		},
		methods: {
			calcHeight() {
				this.panelHeight = this.$refs.carouselProjects.clientHeight;
			},
			calcOffset() {
				let offset = this.panelsDisplayed * this.marginWidth;
				offset += this.panelWidth;
				offset *= this.location;
				return offset;
			},
			offset(i) {
				let offset = this.calcOffset();
				let offsetDelay = (i - this.location) * 25; // TODO alter based on direction
				return `transition-delay: ${ offsetDelay }ms; transform: translateX(  calc(10vw - ${ offset }%) );`;
			},
			saturate(i) {
				//console.log(i+" | "+this.location);
				return {
					faded: (i < this.location) || (i > this.location + this.panelsDisplayed-1),
				};
			},
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
	.arrows{
		margin: 1em 0px; 
	}
	.arrow {
		display: inline;
		font-size: 2em;
		color: white;
		transition: color 0.2s;
		&:hover{
			cursor: pointer;
		}
		&.left:before{
			content: "<";
		}
		&.right{
			float: right;
			&:before{
				content: ">";
			}
		}
		&.active{
			color: $highlight;
		}		
	}

	.project-carousel{
		//see setHeight()
		height: 0px;
	}

	.projects{
		display: flex;
		position: absolute;
		width: 100%;
		left: 0;
		overflow: hidden;

		&.one-panel{
			.project{
				width: 80%;
				min-width: 80%;
			}
		}

		&.two-panel{
			.project{
				width: 37.5%;
				min-width: 37.5%;
			}
		}

		&.three-panel{
			.project{
				width: 23.33%;
				min-width: 23.33%;
			}
		}
	}

	.project{
		transition-timing-function: ease-in;
		transition: transform 450ms;
		transform: translateX(calc(10vw - 0%));
		margin-right: 5%; 

		.overlay{
			background: $background;
			opacity: 0.0;
			transition: opacity 200ms, transform 200ms;
			position: absolute;
			top:0;
			left:0;
			right:0;
			bottom: 0;
			visibility: hidden
		}
	}

	.project-description{
		min-height: 250px;
		background: $background;
		padding: 1.5em;
		transform-origin: bottom;
		transition: transform 200ms;
		.project-title{
			font-size: 2.5em;
			margin-bottom: 0.5em;
			overflow: hidden;
			display: flex;
			span{
				transition: opacity 300ms 200ms, transform 400ms 200ms;
			}
		}
		.project-summary{
			transition: opacity 300ms 400ms, transform 300ms 400ms;
			font-size: 0.8em;
		}
	}

	.project-image{
		width: 100%;
		height: 300px;
		background: $highlight;
		transform-origin: top;
		transition: background-color 200ms, transform 200ms;
		position: relative;
	}

	

	.view-code-btn {
		padding: 0.5em;
		position: absolute;
		bottom: 0;
		display: flex;
		transform: translate(1em, -0.5em);
		color: $alt-background;
		text-decoration: none;
		&:before{
			content: "<";
		}
		&:after{
			content: " />";
		}
		span{
			transition: max-width 0.2s, color 0.2s;
			max-width: 0px;
			overflow: hidden;
			white-space: nowrap;
		}

		&:hover {
			color: $background;
			span{
				max-width: 100%;
			}
		}
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

	.faded{
		.overlay{
			transform: scale(0.95);
			opacity: 0.5;
			visibility: visible;
		} 
		.project-description,
		.project-image{
			transform: scale(0.95);
			.project-title span{
				opacity: 0.0;
				transform: translateY(1em);
			}
			.project-summary{
				opacity: 0.0;
				transform: translateY(1em);
			}
		}

		.live-site-btn{
			span{
				transform: translate(0em, 1em);
			}
		}
	}

</style>