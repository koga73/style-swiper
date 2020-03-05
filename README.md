# style-swiper
Add JS pagination and arrows to a pure CSS swiper

Supports IE11+ with progressive enhancement - that is IE11 only snaps to items when scrolling via Touch

## HTML
```html
<!-- Required: Container -->
<div id="myStyleSwiper" class="style-swiper-container">
	<!-- Optional: This div just lets the buttons vertically center with the slides minus the pagination  -->
	<div class="style-swiper-slide-btn-wrap">

		<!-- Optional: Previous button -->
		<button class="style-swiper-btn-prev">
			<i class="fa fa-chevron-left"><!-- FontAwesome Icon--></i>
			<span class="seo">scroll previous</span>
		</button>

		<!-- Required: Slides -->
		<div class="style-swiper-slides hide-scrollbar">
			<div>Slide 1</div>
			<div>Slide 2</div>
			<div>Slide 3</div>
		</div>

		<!-- Optional: Next button -->
		<button class="style-swiper-btn-next">
			<i class="fa fa-chevron-right"><!-- FontAwesome Icon--></i>
			<span class="seo">scroll next</span>
		</button>

	</div>

	<!-- Optional: Pagination -->
	<ol class="style-swiper-pagination"></ol>
</div>
```

## JS
```javascript
var styleSwiper = new StyleSwiper({
	el:document.getElementById("myStyleSwiper")
});
```

## CSS
```css
/* Container */
.style-swiper-container {
	position:relative;
	text-align:center;
}

.style-swiper-slide-btn-wrap {
	position:relative;
}

/* Slides */
.style-swiper-slides {
	display:flex;
	overflow-x:auto;
	scroll-snap-type:mandatory; /* Fallback if "x" not supported */
	scroll-snap-type:x mandatory;
	-ms-scroll-snap-type:mandatory;
	-webkit-scroll-snap-type:mandatory;
	-webkit-scroll-snap-destination:0% 0%;
	-webkit-overflow-scrolling:touch;
	/* Note:IE11 only supports touch - graceful fallback is standard scroll area */
}
.style-swiper-slides > * {
	flex-shrink:0;
	max-width:100%;
	scroll-snap-align:start;
}

/* Buttons */
.style-swiper-btn-prev, .style-swiper-btn-next {
	position:absolute;
	top:50%;
	transform:translateY(-50%);
	z-index:1;
	background-color:black;
	border:0;
	font-size:2em;
	margin:0;
	padding:0;
	cursor:pointer;
	color:#FFF;
	padding:10px;
	box-sizing:border-box;
}
.style-swiper-btn-prev {
	left:0;
}
.style-swiper-btn-next {
	right:0;
}

/* Pagination */
.style-swiper-pagination {
	display:inline-block;
}
.style-swiper-page {
	display:inline-block;
	width:40px;
	height:10px;
	border-radius:10px;
	background-color:#888;
	opacity:0.5;
	margin:5px;
	cursor:pointer;
}
.style-swiper-page.style-swiper-visible{
	background-color:#F80;
}
.style-swiper-page.style-swiper-active {
	background-color:#00F;
}

/* Scrollbar */
.hide-scrollbar {
	scrollbar-width:none; /* Firefox */
	-ms-overflow-style:none;
}
.hide-scrollbar::-webkit-scrollbar {
	display:none;
}

/* Hidden */
.style-swiper-hidden {
	display:none;
}

/* Visually hide content for SEO and Accessibility */
.seo {
	position:absolute;
	top:0;
	left:0;
	width:0;
	height:0;
	opacity:0;
	font-size:0;
}
```

## API Reference
Any of these can be passed into constructor to override or called on the instance
- **attributePageNum**: String | Attribute to add to page indicating page number | defaullt: *data-page-num*
- **classSlides**: String | Class to select slides | default: *style-swiper-slides*
- **classBtnPrev**: String | Class to select previous button | default: *style-swiper-btn-prev*
- **classBtnNext**: String | Class to select next button | default: *style-swiper-btn-next*
- **classPagination**: String | Class to select pagination container | default: *style-swiper-pagination*
- **classPage**: String | Class to add to generated pages | default: *style-swiper-page*
- **classVisible**: String | Class to add to visible elements | default: *style-swiper-visible*
- **classActive**: String | Class to add to active elements | default: *style-swiper-active*
- **classHidden**: String | Class to add to hidden elements | default: *style-swiper-hidden*
- **classSeo**: String | Class to add visually hidden elements for SEO and Accessibility | default: *seo*

- **scrollBehavior**: String | Behavior of scrollTo | default: *smooth*
- **scrollDebounce**: Number | Time in milliseconds to wait after last scroll event before eval | default: *100*

- **init**: Initialize on a container element | default: *document*
- **destroy**: Clean up instance
- **getSlides**: Get children of element classSlides
- **getVisible**: Get slides with classVisible
- **getActive**: Get slides with classActive
- **getActiveIndex**: Get index of active slide
- **updateSlides**: Re-grab elements in container and cache bounds (cache if resizer present)
- **isVisible**: Returns true if the element argument is currently visible based on element / container bounds comparison
- **evalVisibility**: Check visibility slides / buttons / pages and add classes
- **evalActive**: Find active slide and add classes
- **previous**: Scroll previous slide based on activeIndex
- **next**: Scroll next slide based on activeIndex
- **goto**: Scroll to a specific slide index