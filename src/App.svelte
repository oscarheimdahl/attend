<script>
  import CreateEvent from './CreateEvent.svelte';
  import FindEvent from './FindEvent.svelte';
  import Event from './Event.svelte';
  import config from './firebase_config.js';
  import firebase from 'firebase/app';
  import 'firebase/firestore';
  firebase.initializeApp(config);
  const db = firebase.firestore();

  let showingEvent = false;
  let eventID;
  const showEvent = (event) => {
    eventID = event.detail.eventID;
    showingEvent = true;
  };
</script>

<main>
  {#if !showingEvent}
    <CreateEvent on:showEvent={showEvent} setShowEvent={showEvent} {db} />
    <FindEvent on:showEvent={showEvent} {db} />
  {/if}
  {#if showingEvent}
    <Event {eventID} {db} />
  {/if}
</main>

<style>
</style>
