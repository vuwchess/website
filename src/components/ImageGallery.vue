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
  <Galleria :value="images" :responsiveOptions="responsiveOptions" :numVisible="5" :circular="true"
    containerStyle="max-width: 640px" :showItemNavigators="true" :showThumbnails="false" :showItemNavigatorsOnHover="true"
    :showIndicators="true">
    <template #item="slotProps">
      <img :src="slotProps.item.source.url" :alt="slotProps.item.title" class="gallery-image"
        style="width: 100%; display: block; border-radius: 25px" />
    </template>
  </Galleria>
</template>