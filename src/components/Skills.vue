<template>
	<div class="skills block">
		<h2 class="block-title">Skills</h2>
		<section class="sub-section">
			<div class="skill-set" 
				v-for="skillSet in skillSets" 
				v-bind:key="skillSet.name"
				>
				<h3>{{ skillSet.name }}:</h3>
				<ul>
					<li class="skill"
						v-for="skill of skillSet.skills"
						v-bind:key="skill"
						>
						{{ skill }}
					</li>
				</ul>
			</div>
		</section>
	</div>
</template>

<script>
	export default {
		name: 'Skills',
		props: {
			skillSets: Array,
		}
	}
</script>

<style lang="scss" scoped>
	.skills{
		.sub-section{
			display: flex;
			flex-wrap: wrap;
			justify-content: flex-start;
			align-items: baseline;
		}
	}
	.skill-set{
		min-width: 10%;
		margin: 0 3em 2em 0;

		ul{
			list-style: none;
		}

		h3 {
			font-size: 1em;
			margin-bottom:0.5em;
		}

		li{
			font-size: 0.8em;
		}
	}
</style>