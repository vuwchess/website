<script lang="ts" >
import Galleria from 'primevue/galleria';
import 'primevue/resources/themes/saga-green/theme.css';
export default {
  components: {
    Galleria,
  },
  data() {
    return {
      images: [],
      responsiveOptions: [
        {
          breakpoint: '991px',
          numVisible: 4
        },
        {
          breakpoint: '767px',
          numVisible: 3
        },
        {
          breakpoint: '575px',
          numVisible: 1
        }
      ]
    };
  },
  async created() {
    this.images = await this.getImages();
  },
  methods: {
    getImages: async () => {
      const query = `{
        imageGalleryPhotoItemCollection {
          items {
            sys {
              id
            }
            title
            source {
              title
              description
              url
            }
          }
        }
      }`;
      const fetchUrl = `https://graphql.contentful.com/content/v1/spaces/${import.meta.env.VITE_CONTENTFUL_SPACE_ID}`;
      const fetchOptions = {
        method: "POST",
        headers: {
          Authorization: `Bearer ${import.meta.env.VITE_CONTENTFUL_ACCESS_TOKEN}`,
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ query })
      };

      try {
        const response = await fetch(fetchUrl, fetchOptions).then(response =>
          response.json()
        );
        return response.data.imageGalleryPhotoItemCollection.items;
      } catch (error) {
        throw new Error("Could not receive the data from Contentful!");
      }
    }
  }
};
</script>

<template>
  <div class="card">
    <Galleria :value="images" :responsiveOptions="responsiveOptions" :numVisible="5" :circular="true"
      :showItemNavigators="true" :showThumbnails="false" :showItemNavigatorsOnHover="false" :showIndicatorsOnItem="false"
      :showIndicators="true">
      <template #item="slotProps">
        <img :src="slotProps.item.source.url" :alt="slotProps.item.source.description" class="gallery-image" />
      </template>
    </Galleria>
  </div>
</template>

<style scoped>
.card {
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
  border-radius: 25px;
  background-color: var(--background-color);
}

.gallery-image {
  display: block;
  border-radius: 25px 25px 0px 0px;
  width: 100%;
  height: 350px;
  object-fit: cover;
}
</style>