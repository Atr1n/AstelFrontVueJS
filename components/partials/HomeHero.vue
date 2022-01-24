<template>
	
	<div class="start-hero">
		<carousel :responsive="responsive">
			<template slot="prev">
				<span class="btn btn-prev"> &#10094;</span>
			</template>
			<div v-for="n of 5" :key="n">
				<img class="hero_main_img" :src="$page()['image'+`${n}`]">
				<div class="hero_main_wrap">
					<h1 class="hero_main_title">{{ $page()['title'+`${n}`] }}</h1>
					<div class="hero_main_text" v-if="n === 3">
						<p>{{ $page()['description'+`${n}`] }}</p>
					</div>
					<div class="hero_main_text" v-else>
						<p>{{ $page()['description'+`${n}`] }}</p>
					</div>
					<component
						:is="isSameHost($page()['link'+`${n}`]) ? 'nuxt-link' : 'a'"
						:href="isSameHost($page()['link'+`${n}`]) ? $url($page()['link'+`${n}`]) : $page()['link'+`${n}`]"
						:to="$url($page()['link'+`${n}`])" class="hero_main_btn buttonHome --blue animate-home-hero buttonHome-hover"
						data-on-scroll-paginate
						v-if="$page()['link'+`${n}`]">{{ $trans('Подробнее') }}
					</component>
				</div>
			</div>
			<template slot="next">
				<span class="btn btn-next"> &#10095;</span>
			</template>
		</carousel>
	</div>

</template>


<script>
import {gsap} from "gsap";


export default {
	props: ['timeline'],
	mounted() {
		this.animateOnLoad();
	},
	data() {
		return {
			responsive: {
				0: {items: 1, nav: false, autoplay: false},
				600: {items: 1, nav: false, autoplay: false},
				900: {items: 1, nav: false, autoplay: false}
			}
		}
	},
	methods: {

		// counter(event) {
		//
		// 	let element = event.target; // DOM element, in this example .owl-carousel
		// 	let items = event.item.count; // Number of items
		// 	let item = event.item.index + 1; // Position of the current item
		//
		// 	// it loop is true then reset counter from 1
		// 	if (item > items) {
		// 		item = item - items
		// 	}
		// 	$(element).parent().find('.counter').html("item " + item + " of " + items)
		// },
		getMime(url) {
			let chunks = url.split('.')
			return `video/${chunks[chunks.length - 1]}`
		},
		isSameHost(url) {
			return !url.startsWith('http')
		},
		animateOnLoad() {
			// let tl = this.timeline;
			//let tl = gsap.timeline();
			let tl = gsap;
			let header = document.querySelector(".layout-content");
			//let item = header.querySelectorAll("[data-on-scroll-paginate]");
			let item = document.querySelectorAll(".animate-home-hero");
			tl.fromTo(
				item,
				{opacity: 0, y: 30},
				{
					opacity: 1,
					y: 0,
					stagger: 0.25,
					delay: 0.1,
					duration: 2.6,
					ease: "elastic",
				},
				'hero'
			);
		}
	}
};
</script>

<style lang="sass">
.hero_main_wrap
	position: absolute
	top: 10rem
	left: 13rem
	@media (max-width: 450px)
		top: 5rem
		left: 1rem
		height: 50vh
		object-fit: cover

.hero_main_img
	@media (max-width: 450px)
		height: 50vh
		object-fit: cover 

.hero_main_title
	width: 450px
	margin-bottom: 1rem
	color:#bf0d0d
	@media (max-width: 450px)
		width: 320px 
		margin-bottom: 0
		font-size: 20px

.hero_main_text
	p 
		width: 420px
		font-family: Calibri,serif
		font-size: 21px
		@media (max-width: 450px)
			font-size: 16px

.hero_main_btn 
	@media (max-width: 450px)	
		margin: 0
		margin-top: 2rem
		line-height: 30px

/* GO TO NEXT SLIDE */
.slide-next-enter-active,
.slide-next-leave-active
	transition: transform 0.5s ease-in-out

.slide-next-enter
	transform: translate(100%)

.slide-next-leave-to
	transform: translate(-100%)


/* GO TO PREVIOUS SLIDE */
.slide-prev-enter-active,
.slide-prev-leave-active
	transition: transform 0.5s ease-in-out

.slide-prev-enter
	transform: translate(-100%)

.slide-prev-leave-to
	transform: translate(100%)

.btn
	z-index: 10
	cursor: pointer
	border: 3px solid #939292
	color: #939292
	display: flex
	justify-content: center
	align-items: center
	width: 70px
	height: 70px
	position: absolute
	top: calc(50% - 35px)
	left: 1%
	transition: transform 0.3s ease-in-out
	user-select: none
	@media (max-width: 450px)
		display: none

.btn-next
	left: auto
	right: 1%


.btn:hover
	transform: scale(1.1)


.home-hero
	position: relative

	&-bg-video
		position: absolute
		top: 0
		left: 0
		width: 100%
		height: 100%
		object-fit: cover

	&-inner
		position: relative
		z-index: 1
		background: rgba(#000, 0.3)
		min-height: calc(100vh - 140px)
		display: flex
		align-items: center
		justify-content: center

	&-subtitle
		color: #fff
		font-size: 14px
		font-weight: 700
		margin-bottom: 20px

	&-title
		color: #fff
		font-size: 48px
		font-weight: 700
		max-width: 706px
		margin-bottom: 20px
		line-height: 59px

	&-text
		max-width: 609px
		font-size: 18px
		font-weight: 300
		color: #fff
		margin-bottom: 20px


@media (min-width: 320px)
	.home-hero
		&-inner
			padding: 40px 10px
			min-height: 50vh

		&-title
			font-size: 20px
			line-height: initial
			margin-bottom: 15px

		&-text
			font-size: 14px

		&-subtitle,
		&-text
			margin-bottom: 15px

@media (min-width: 1280px)
	.home-hero
		&-inner
			padding: 0
			min-height: calc(100vh - 120px)

		&-title
			font-size: 36px
			margin-bottom: 15px

		&-text
			font-size: 16px

		&-subtitle,
		&-text
			margin-bottom: 15px
</style>
