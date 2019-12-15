<template>
  <div class="experience block">
    <h2 class="block-title">
      Experience
    </h2>
    <!-- loop through jobs -->
    <div
      v-for="(job, index) in jobs" 
      :key="index" 
      class="job"
    >	
      <section
        v-if="job.type === 'carousel'"
        class="sub-section alt carousel"
      >
        <div
          class="job"
          layout="carousel"
        >
          <div class="job-description">
            <h3 class="job-title">
              {{ job.title }}
            </h3>
            <h4 class="job-sub-title">
              {{ job.company }} | {{ job.date }}
            </h4>
            <p class="job-summary">
              {{ job.summary }}
            </p>
          </div>
          <Carousel :projects="job.projects" />
        </div>
      </section>

      <section
        v-else-if="job.type === 'slideshow'"
        class="sub-section slideshow"
      >
        <div
          class="job"
          layout="slideshow"
        >
          <div class="job-description">
            <h3 class="job-title">
              {{ job.title }}
            </h3>
            <h4 class="job-sub-title">
              {{ job.company }} | {{ job.date }}
            </h4>
            <p class="job-summary">
              {{ job.summary }}
            </p>
          </div>
						
          <Slider :slides="job.slides" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
	import Carousel from '@/components/experience/Carousel.vue'
	import Slider from '@/components/experience/Slider.vue'

	export default {
	name: 'Experience',
	components: {
		Carousel,
		Slider,
	},
	props: {
		jobs: {
			type: Array,
			default() {
				return []
			}
		}
	}
}
</script>

<style lang="scss" scoped>
	@import "@/assets/scss/global-vars.scss";

	.job-description{
		margin-bottom: 2em;

		.job-title{
			margin-bottom: 0.3em;
		}

		.job-sub-title{
			margin-bottom: 1em;
			font-weight: normal;
			color: $highlight;
		}

		.job-summary{
			max-width: 700px;
		}
	}

	.sub-section.carousel{
		overflow-x: hidden;
	}

	.carousel{
		margin-bottom: 200px;
	}

	.slideshow .job{
		display: flex;
		align-items: center;
		.job-description{
			width: 46.875%;
			margin-right: 6.25%;
		}
		.slider {
			width: 46.875%;
		}
	}

</style>