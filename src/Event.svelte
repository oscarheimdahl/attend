<script>
  export let db;
  export let eventID;
  let eventName;
  let attendees = [];
  let name = '';
  db.collection('events')
    .doc(eventID)
    .onSnapshot((doc) => {
      eventName = doc.data().name;
      attendees = doc.data().attendees;
      if (!attendees) attendees = [];
    });

  const joinEvent = () => {
    db.collection('events')
      .doc(eventID)
      .set({ attendees: [name, ...attendees] }, { merge: true });
  };
</script>

<main>
  <h2>{eventName ?? ''}</h2>
  {#each attendees as attendee}
    {#if attendee === 'Oscar'}
      <p>{attendee + ' (You)'}</p>
    {:else}
      <p>{attendee}</p>
    {/if}
  {/each}
  <input bind:value={name} type="text" placeholder="Name" />
  <button on:click={joinEvent}>Join</button>
</main>

<style>
</style>
