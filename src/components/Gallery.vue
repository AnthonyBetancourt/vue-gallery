<template>
	<div class="gallery-container">
		<h1>Image Gallery</h1>
		<SearchInput v-model="search"/>
		<div class="card-container">
			<div class="image-card" v-for="(image, index) in filteredImages" :key="index" @click="showModal(image)">
				<img :src="image.url_sq" @error=imageUrlAlt class="image-card-img" />
				<div class="image-card-content">{{image.title}}</div>
			</div>
			<Modal :image="selectedItem" @closeModal="closeModal"/>
		</div>
		<Pagination v-on:prevPage="prevPage" v-on:nextPage="nextPage"></Pagination>
	</div>
</template>

<script>
import json from '../json/data.json';
import SearchInput from './SearchInput.vue';
import Pagination from './Pagination.vue';
import Modal from './Modal.vue';
export default {
	name: 'Gallery',
	components: {
		SearchInput,
		Pagination,
		Modal
	},
	data: function() {
		let newArray = json.photos.photo;
		return {
			images: newArray,
			search: '',
			current_page: 1,
			images_per_page: 8,
			resultsArray: [],
			modalOpen: false,
			selectedItem: undefined
		};
	},
	methods: {
		imageUrlAlt(event) {
			event.target.src = "https://via.placeholder.com/240x240?text=Unavailble";
		},
		prevPage: function() {
			if (this.current_page > 1) {
				this.resultsArray = [];
				this.current_page--;
				this.updatePage(this.current_page);
			}
		},
		nextPage: function() {
			if (this.current_page < this.totalPages()) {
				this.resultsArray = [];
				this.current_page++;
				this.updatePage(this.current_page);
			}
		},
		updatePage: function(page) {
			let btn_next = document.getElementById("btn_next");
			let btn_prev = document.getElementById("btn_prev");
			let page_span = document.getElementById("page");
			let images = this.images;

			// Validate page
			if (page < 1) page = 1;
			if (page > this.totalPages()) page = this.totalPages();

			for (let i = (page - 1) * this.images_per_page; i < (page * this.images_per_page) && i < images.length; i++) {
				let resultsArray = this.resultsArray;
				console.log("for ", i);
				resultsArray.push(images[i]);
			}
			page_span.innerHTML = page + " of " + this.totalPages();

			if (page == 1) {
				btn_prev.style.visibility = "hidden";
			} else {
				btn_prev.style.visibility = "visible";
			}

			if (page == this.totalPages()) {
				btn_next.style.visibility = "hidden";
			} else {
				btn_next.style.visibility = "visible";
			}
		},
		totalPages: function() {
			let images = this.images;
			return Math.ceil(images.length / this.images_per_page);
		},
		showModal: function(image) {
			this.selectedItem = image;
			let imageDetail = document.querySelector(".image-detail-container");
			let overlay = document.querySelector(".overlay");
			imageDetail.classList.remove("hide");
			overlay.classList.remove("hide");
		},
		closeModal: function() {
			let imageDetail = document.querySelector(".image-detail-container");
			let overlay = document.querySelector(".overlay");
			imageDetail.classList.add("hide");
			overlay.classList.add("hide");
		}
	},
	mounted() {
		this.updatePage(1);
	},
	computed: {
		filteredImages: function() {
			let self = this;
			let resultsArray = this.resultsArray;
			return resultsArray.filter(function(el) {
				return el.title.toLowerCase().indexOf(self.search.toLowerCase()) >= 0;
			});
		}
	}
}
</script>
