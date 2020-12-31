<template>
  <h1>Events for Good</h1>
  <div class="events">
    <EventCard
      v-for="event in events"
      :event="event"
      :key="event.id"
    />
  </div>
</template>

<script>
  import EventCard from '@/components/EventCard.vue';
  import EventService from '@/services/EventService.js';
  export default {
    name: 'EventList',
    components: { EventCard },
    data() {
      return { events: null };
    },
    created() {
      EventService.getEvents()
        .then( ( { data } ) => {
          console.log( data );
          this.events = data;
        } )
        .catch( error => {
          console.log( error );
        } );
    },
  };
</script>
<style scoped>
  .events {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
