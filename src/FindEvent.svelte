<script>
  export let db;
  let eventID;
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  const findEvent = async (e) => {
    e.preventDefault();
    const doc = await db.collection('events').doc(eventID).get();
    if (!doc.exists) return;
    dispatch('showEvent', { eventID });
  };
</script>

<main>
  <h2>Find event.</h2>
  <form>
    <input bind:value={eventID} type="text" placeholder="Event Code..." />
    <button on:click={findEvent}>Search</button>
  </form>
</main>

<style>
</style>
