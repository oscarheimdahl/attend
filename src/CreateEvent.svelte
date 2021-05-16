<script>
  export let db;
  // import { createEventDispatcher } from 'svelte';
  // const dispatch = createEventDispatcher();
  import { hri } from 'human-readable-ids';
  let eventName;
  let eventID;
  const createEvent = async (e) => {
    e.preventDefault();
    eventID = hri.random();
    await db.collection('events').doc(eventID).set({
      name: eventName,
    });
    // window.history.pushState('', '', eventID);

    // dispatch('showEvent', { eventID });
  };
</script>

<main>
  <h2>Create new event!</h2>
  <form>
    <input bind:value={eventName} type="text" placeholder="Balloon Party!" />
    <button on:click={createEvent}>Create</button>
    {#if eventID}
      <h3>Event ID: {eventID}</h3>
    {/if}
  </form>
</main>

<style>
</style>
