<script>
  import CreateEvent from './CreateEvent.svelte';
  import FindEvent from './FindEvent.svelte';
  import ShowEvent from './ShowEvent.svelte';
  import config from './firebase_config.js';
  import firebase from 'firebase/app';
  import 'firebase/firestore';
  firebase.initializeApp(config);
  const db = firebase.firestore();

  let eventID;
  const showEvent = (event) => {
    eventID = event.detail.eventID;
  };
  console.log(window.location.pathname);
</script>

<main>
  {#if !eventID}
    <CreateEvent setShowEvent={showEvent} {db} />
    <FindEvent on:showEvent={showEvent} {db} />
  {:else}
    <ShowEvent on:showEvent={showEvent} {eventID} {db} />
  {/if}
</main>

<style>
</style>
