<template>
  <div>
    <Header 
      title="George Baldwin"
      :summary="summery"
    />
    <Skills :skill-sets="skillSets" />
    <Experience :jobs="experience" />
  </div>
</template>

<script>
	import Header from '../components/Header.vue'
	import Skills from '../components/Skills.vue'
	import Experience from '../components/Experience.vue'
	//import Contact from './components/Contact.vue'

	export default {
		name: 'CV',
		components:{
			Header,
			Skills,
			Experience,
		},
		data: function() {
			return {
				title: "George Baldwin",
				summery: "Creative front-end web developer with a background in the arts. Looking for a permanent role in a digital/creative agency based in Bristol.",
				skillSets: [
					{
						name: "Languages",
						skills: ["Html", "Css (Sass)", "Javascript (ES6+)", "glsl", "PHP", "Java", "C++"]
					},
					{
						name: "Javascript",
						skills: ["Vuejs", "Webgl (threejs)", "Greensock", "Matter.js", "P5*js", "Jquery", "GraphQL (Apollo)", "Nodejs"]
					},
					{
						name: "Backend / CMS",
						skills: [ "NPM", "Expressjs", "Webpack", "Gulp"]
					},
					{
						name: "Build Tool",
						skills: ["Html", "Css (Sass)", "Javascript (ES6+)", "glsl", "PHP", "Java", "C++"]
					},
					{
						name: "Software",
						skills: ["Photoshop", "Illustrator", "After Effects", "Premiere", "Sketchup", "Figma"]
					},
				],
				experience: [
					{
						type: "carousel",
						title: "Web Developer/Designer",
						company: "freelance",
						date: "2017 - current",
						summary: "I’ve worked predominantly with local small businesses and start-ups. I possess strong knowledge of the web foundations and utilise modern javascript tools to speed up the process and make the user experience more engaging.",
						projects: [
							{
								company: "Hool Festival",
								summary: "I was approached to prototype functionality of an online digital arts festival and to test feasibility. Working alongside an animator we researched workflows and I built out a browser based 3-D experience. I developed specific functionality including custom camera movements, interactions with the art pieces and a custom shaders. Utilising Firebase I created a near real time multiplayer experience with avatars. I also designed and developed the current splash page. Using a custom shader to animate the visuals and mailchimp to store signups. All made with vuejs, threejs and hosted on Ziet. ", 
								codeURL: "#",
								link: {
									label: "hoolfest.com",
									url: "https://hoolfest.com"
								},
								image: {
									url: "#",
									alt: "",
								},
							},
							{
								company: "Firewok",
								summary: "The brief was to update their 4 year old Wordpress website and improve the branding and useability. Using Wordpressify I developed a child theme to work with Storefront and Woocommerce. Utilising Advanced Custom Fields plugin I created custom blocks with specific functionality. This replaced a bulky site builder plugin helping to speed up the website and make it easier to use. The design of the site was refined and mobile useability was greatly improved. I also reshot all of the products to give them a consistent look.", 
								codeURL: "#",
								link: {
									label: "firwok.co.uk",
									url: "https://firewok.co.uk"
								},
								image: {
									url: "#",
									alt: "",
								},
							},
							{
								company: "Hub at No.3",
								summary: "I came on board to help with a new squarespace website they had started. I designed the layout and  restructured the overall site to make it easier to navigate. I embed Checkfront into the booking pages allowing users to book events and rooms. Added custom css I kept the overall design cohesive. I delivered training on how to use Squarespace, Checkfront and integrated the booking system into their till system.", 
								codeURL: "#",
								link: {
									label: "hubatno3.co.uk",
									url: "https://hubatno3.co.uk"
								},
								image: {
									url: "#",
									alt: "",
								},
							},
						]
					},
					{
						type: "slideshow",
						title: "Artist",
						company: "eegb",
						date: "2014 - current",
						summary: "Eegb was formed by Edmund Eva and myself after meeting at Falmouth University. We have since gone on to attend a number of artist residencies, given talks and exhibited in the UK, Ireland, Germany and the USA.",
						slides: [
							{ 
								link: {
									label: "Gestalt, 2018",
									url: "https://hoolfest.com"
								},
								image: {
									url: "#",
									alt: "",
								},
							},
							{ 
								link: {
									label: "Gestalt, 2018",
									url: "https://hoolfest.com"
								},
								image: {
									url: "#",
									alt: "",
								},
							},
							{ 
								link: {
									label: "Gestalt, 2018",
									url: "https://hoolfest.com"
								},
								image: {
									url: "#",
									alt: "",
								},
							},
						]
					},
				],

			};
		},
	}
</script>

<style lang="scss" scoped>
	
</style>