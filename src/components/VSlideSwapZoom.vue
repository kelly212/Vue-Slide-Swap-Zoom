<template>
			<div style="border: 1px grey dashed; ">
						<v-row>
									<v-col v-if="is_vertical" cols="12" sm="12" md="3" lg="2" style="width: 100%; ">
												<div style="max-height: 400px; align-content: center">
															<v-tabs v-if="images.length > 0" direction="vertical" center-active slider-color="orange"
																							prev-icon="mdi-chevron-up" next-icon="mdi-chevron-down">
																		<v-tab v-for="(img, index) in images" :value="index" @click="selecionar(index)" height="60px">
																					<v-icon aria-label="slide" style="width: 100px; height: auto; margin-left: 15%">
																								<v-img loading="lazy"  defer :src="img.url" cover height="50"  :alt="'slide_'+index"></v-img>
																					</v-icon>
																		</v-tab>
															</v-tabs>
												</div>
									</v-col>
									<v-col cols="12" sm="12" :md="is_vertical? 9 : 12" :lg="is_vertical? 10 : 12" style="width: 100%; ">
												<div style="width: 100%; max-height: 400px">
															
															<vue-photo-zoom-pro  v-if="is_magnify "    :highUrl="images[currentSlide].url">
																		<div class="imagem-container">
																					<img defer :src="images[currentSlide].url" alt="Descrição da imagem">
																		</div>
															
															</vue-photo-zoom-pro>
															
															<vue-photo-zoom-pro v-else  :width="selectWidth" :height="selectHeight"
																																			@update="handleUpdate"
																																			:highUrl="images[currentSlide].url ">
																		<div class="imagem-container">
																					<img defer :src="images[currentSlide].url" alt="Descrição da imagem">
																		</div>
															
															</vue-photo-zoom-pro>
												
												</div>
									</v-col>
									
									
									<v-col v-if="!is_vertical" cols="12" style="width: 100%;">
												<v-tabs v-if="images.length > 0" height="100px">
															<v-tab v-for="(img, index) in images" :value="index" @click="selecionar(index)" align-tabs="center">
																		<v-icon aria-label="image" style="width: 80px; height: auto">
																					<v-img loading="lazy"  defer :src="img.url" cover  width="auto" height="50" :alt="'slides_'+index"></v-img>
																		</v-icon>
															</v-tab>
												</v-tabs>
									</v-col>
						</v-row>
			</div>
</template>

<script defer>
   /* eslint-disable */
   import {Carousel, Slide, Navigation} from "vue3-carousel";
   import VuePhotoZoomPro from 'vue-photo-zoom-pro'


   export default {
      name: "VSlideSwapZoom",
      props: {
         is_magnify: {default: false},
         is_vertical: {default: false},
         images: {default: []},
      },
      components: {
         VuePhotoZoomPro,
         Carousel,
         Slide,
         // Pagination,
         Navigation
      },
      data: () => ({
   
         // images: [],
         thumbnailsConfigV: {
            dir: 'ttb',
            wrapAround: true,
            itemsToShow: 5,
            snapAlign: 'top',
            gap: 1,
         },
         thumbnailsConfig: {
            itemsToShow: 6,
            wrapAround: true,
            snapAlign: 'top',
            gap: 10,
         },
         galleryConfig: {
            itemsToShow: 1,
            wrapAround: true,
            mouseDrag: false,
            touchDrag: false,
         },
         currentSlide: 0,
         selectWidth: 0,
         selectHeight: 0,
      }),
      methods: {
         slideTo(nextSlide) {
            this.currentSlide = nextSlide
         },
         selecionar(index) {
            this.currentSlide = index

         },
         UpOrDown(is_up = false) {
            if (is_up) {
               if (this.currentSlide > 0) {
                  this.currentSlide--
               }

            } else {
               if (this.currentSlide < this.images.length - 1) {
                  this.currentSlide++
               }

            }
         },
         handleUpdate(e) {
            this.selectWidth = e.width
            this.selectHeight = e.height
         },
      },
   }
</script>

<style lang="scss" scoped>
			.vue-photo-zoom-pro {
						width: 100%;
			}
			.selector{
						border: 1px solid rgba(94, 94, 94, 0.3);
			}
			
			.imagem-container {
						width: 100%;
						height: 400px;
						overflow: hidden;
						position: relative;
			}
			
			.imagem-container img {
						width: 100%;
						height: 100%;
						object-fit: cover;
						display: block;
			}
			
			#gallery_v {
						.vue-magnifier__magnifier {
									width: auto !important;
									height: 100% !important;
						}
						
						.carousel__item, .gallery-image {
									width: 100%;
									/*height: 400px;*/
									height: 100% !important;
						}
						
			}
			
			.zoom_produto {
						img {
									/*height: 400px!important;*/
						}
			}
			
			#thumbnails_v {
						.carousel__item {
									padding: 1%;
									width: 100%;
									height: 70px;
						}
						
						.carousel__slide--active img {
									border: 2px solid #0ECB81;
						}
						
			}
			
			#gallery {
						.vue-magnifier__magnifier {
									width: auto !important;
									height: 100% !important;
						}
						
						.carousel__item, .gallery-image {
									width: 100%;
									height: 400px;
						}
			}
			
			#thumbnails {
						.carousel__item {
									padding: 1%;
									width: 100%;
									height: 100px;
						}
						
						.carousel__slide--active img {
									border: 2px solid #0ECB81;
						}
			}


</style>
