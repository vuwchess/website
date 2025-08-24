<script lang="ts">
import { Calendar } from 'v-calendar';
import 'primevue/resources/themes/saga-green/theme.css';
export default {
    components: {
        Calendar,
    },
    data() {
        return {
            events: [],
            selectedColor: 'green',
        };
    },
    async created() {
        this.events = (await this.getEvents());
    },
    methods: {
        getEvents: async () => {
            const query = `{
        eventCollection {
          items {
            sys {
              id
            }
            title
            startDateTime
            endDateTime
            description
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
                return response.data.eventCollection.items;
            } catch (error) {
                throw new Error("Could not receive the data from Contentful!");
            }
        }
    }
};
</script>

<template>
    <div class="events-container">
        <Calendar :color="selectedColor" />
        <div v-for="event in events" :key="event" class="event">
            <h2>{{ event["title"] }}</h2>
            <div class="card">

            </div>
        </div>
    </div>
</template>

<style scoped>
.events-container {
    display: flex;
    flex-direction: column;
    gap: 40px;
}

.event {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.card {
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    border-radius: 25px;
    background-color: var(--background-color);
    width: 100%;
}
</style>