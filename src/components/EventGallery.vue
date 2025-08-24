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
            attributes: [],
            selectedColor: 'green',
        };
    },
    async created() {
        this.events = (await this.getEvents()).filter((event: any) => new Date() < new Date(event["startDateTime"])).sort((a: any, b: any) => new Date(a["endDateTime"]) > new Date(b["endDateTime"]) ? 1 : -1);
        const dates = this.events.map((event) => [new Date(event["startDateTime"]), new Date(event["endDateTime"])])
        this.attributes = [{
            highlight: 'green',
            dates,
        }] as any
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
    <div class="calendar-container">
        <Calendar class="my-calendar" transparent is-dark="system" :attributes="attributes" />
        <div class="events-container">
            <div v-for="event in events" :key="event" class="card">
                <div class="content">
                    <h2>{{ event["title"] }}</h2>
                    <div>{{ event["description"] }}</div>
                </div>
                <div class="date">
                    <div>{{ new Date(event["startDateTime"]).toLocaleString('en-NZ', {
                        day: '2-digit',
                        month: '2-digit',
                        year: '2-digit',
                        hour12: true, hour: 'numeric',
                        minute: '2-digit'
                    }) }}</div>
                    -
                    <div>{{ new Date(event["startDateTime"]).toDateString() !== new
                        Date(event["endDateTime"]).toDateString() ? new
                            Date(event["endDateTime"]).toLocaleString('en-NZ') :
                        new Date(event["endDateTime"]).toLocaleTimeString('en-NZ', {
                            hour12: true, hour: 'numeric',
                            minute: '2-digit'
                        })
                    }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
.my-calendar {
    border-color: var(--color-border);
    color: var(--color-text);
}

.my-calendar .vc-weekday {
    color: hsla(160, 100%, 37%, 1);
}

.my-calendar button {
    background-color: var(--background-color);
    ;
}
</style>
<style scoped>
h2 {
    font-size: 1.2rem;
    font-weight: 500;
    margin-bottom: 0.4rem;
    color: var(--color-heading);
}

.calendar-container {
    display: flex;
    flex-direction: column;
    gap: 40px;
}

.events-container {
    display: flex;
    flex-direction: column;
    gap: 24px;
}

.card {
    box-shadow: 0 0 4px rgba(0, 0, 0, 0.2);
    border: 1px solid var(--color-border);
    border-radius: 25px;
    background-color: var(--background-color);
    width: 100%;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap-reverse;

}

.content {
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.date {
    display: flex;
    gap: 2px;
    color: hsla(160, 100%, 37%, 1);
}
</style>