<template>
	<div class="services-items">
		<div class="services-items-item animate-home-services" data-on-scroll-paginate
			 v-for="(item, index) in services" :key="index">
			<h4 style="margin: 0px 50px 10px 30px;/*position: absolute;*/ color: white;font-size:16px;" class="services-items-title">{{ item.name }}</h4>
			<component style="z-index: 999;position: relative;"
					   :is="isSameHost($pageUrl('services', item.slug)) ? 'nuxt-link' : 'a'"
					   :href="isSameHost($pageUrl('services', item.slug)) ? $url($pageUrl('services', item.slug)) : $pageUrl('services', item.slug)"
					   :to="$url($pageUrl('services', item.slug))" class="buttonMain --blue animate-home-hero buttonMain-hover"
					   data-on-scroll-paginate
					  v-if="item.serviceImages !== null" >
				{{ 'Подробнее' }}
				<!-- <svg width="9" height="6" viewBox="0 0 9 6" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M1 1l3.5 3.5L8 1" stroke="#fff" stroke-linecap="round"></path></svg> -->
			</component>
			<img class="service__item-img" :src="getSrcServiceImage(item.serviceImages)" alt="item.serviceImages">
		</div>
	</div>
</template>

<script>
import { gsap } from "gsap";
import arrow from "@/static/icons/link-arrow.svg"

export default {
	components: {
		arrow,
	},
	props: {
		services: {
			type: Array,
			default: () => []
		},
		timeline: {
			default: null
		}
	},
	data() {
		return {
			urlForImg: 'https://demo-admin.astel.kz/storage/',
			fullUrlImg: '',
			options: {
				slidesPerView: 1,
				spaceBetween: 10,
				watchSlidesVisibility: true,
				navigation: {
					prevEl: ".services-items-prev",
					nextEl: ".services-items-next",
				},
				breakpoints: {
					1024: {
						slidesPerView: 3,
					},
					600: {
						slidesPerView: 2,
					},
				},
			}
		}
	},
	mounted(){
		// this.animateOnLoad();
	},
	methods: {
		getSrcServiceImage (item) {
			this.fullUrlImg =  this.urlForImg.concat(item)
			if (item === null) return ""
			return this.fullUrlImg;
		},
		getMime(url) {
			let chunks = url.split('.')
			return `video/${chunks[chunks.length - 1]}`
		},
		isSameHost(url) {
			return !url.startsWith('http')
		},
		animateOnLoad() {
			//let tl = gsap.timeline();
			let tl = gsap;
			let header = document.querySelector(".layout-content");
			let item = header.querySelectorAll(".animate-home-services");
			tl.fromTo(
				item,
				{ opacity: 0, y: 30 },
				{
					opacity: 1,
					y: 0,
					stagger: 0.25,
					delay: 0.5,
					duration: 2.6,
					ease: "elastic",
				}
			);
		}
	}
}
</script>
<style lang="sass">
.services-items
	display: flex
	&-item
		width: 100%
		max-width: calc(25% - 16px)
		margin-right: 16px
		margin-bottom: 17px
		box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.07)
		background: #fff
		padding: 23px 27px
		transition: background .4s ease
		&:nth-child(4n)
			margin-right: 0
		&:hover
			.services-items-title,
			.services-items-go-to span
				color: #fff
			.services-items-go-to path
				fill: #fff
			.services-items-icon
				background: #10398D
			.services-items-icon-red
				opacity: 0
			.services-items-icon-arrow
				opacity: 1
	&-title
		font-size: 18px
		font-weight: 400
		color: #333333
		margin-bottom: 5px
		transition: color .4s ease
	&-go-to
		display: flex
		align-items: center
		span
			transition: color .4s ease
			font-size: 12px
			font-weight: 300
			text-decoration: underline
			color: $color-red
		svg
			margin-left: 5px
		path
			transition: fill .4s ease
			fill: $color-red
	&-icon
		width: 48px
		height: 48px
		border-radius: 999px
		background: $color-red
		position: relative
		display: flex
		align-items: center
		justify-content: center
		margin-top: 32px
		transition: background .4s ease
		&-red
			transition: opacity .4s ease
			width: 26px
			height: 26px
		&-arrow
			position: absolute
			top: 50%
			left: 50%
			transform: translate(-50%, -50%)
			z-index: 1
			transition: opacity .4s ease
			opacity: 0
@media (min-width: 320px)
	.services-items
		flex-wrap: wrap
		&-item
			max-width: 100%
			margin-right: 0
		&-title
			font-size: 16px
@media (min-width: 700px)
	.services-items
		&-item
			max-width: 49%
			&:nth-child(odd)
				margin-right: 2%
@media (min-width: 1280px)
	.services-items
		&-item
			max-width: calc(33.3% - 16px)
			margin-right: 16px
			&:nth-child(odd)
				margin-right: 16px
			&:nth-child(3n)
				margin-right: 0
			&:nth-child(4n)
				margin-right: 16px
		&-title
			min-height: 50px
.services-items-item.animate-home-services
	width: 15em
	padding: 25px 25px
	color: #fff 
	height: 22em;
	margin: 2em 3.22em 3em 0
	border-radius: 20px
	position: relative
	box-shadow: 5px 5px 5px #8e8a8a 
	background: #01286b url(https://demo-admin.astel.kz//storage/elfinder/test/cell_bg.png) no-repeat
	background-position: 4em 12em
	background-size: 100%
.services-items-item.animate-home-services:nth-child(4n),
.services-items-item.animate-inner-services:nth-child(4n)
	margin-right: 0
.services-items-item.animate-inner-services
	width: 15em
	padding: 25px 25px
	color: #fff
	height: 12.4444em
	margin: 2em 3.22em 3em 0
	border-radius: 20px
	position: relative
	box-shadow: 5px 5px 5px #8e8a8a
	background-size: 100%
	background: #01286b
.services-items-item h4
	display: block
	font-size: 16px
	color: #fff
	min-height: auto
	line-height: 1.5
	position: relative
	margin: 0.5em 1em 1em 0.5em !important;

.services-items-item a
	display: block
	width: fit-content
	position: relative
.services-items-item.animate-inner-services a
	position: absolute !important
    bottom: 25px
.services-items-item .service__item-img
	position: absolute
	max-width: 185px
	bottom: 25px
	right: 25px
	z-index: 0
.services-category .services-items-title
	position: relative !important
</style>
