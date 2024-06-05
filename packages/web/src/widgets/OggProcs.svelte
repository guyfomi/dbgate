<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();  

  let promise = fetchData();

  async function fetchData() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=proc_states');
    const data = await res.json();    

    if (res.ok) {
      return data;
    } else {
      throw new Error();
    }
  }
</script>

<table>
  <tr><th>Processus</th><th>Status</th><th>Latence</th><th></th></tr>

  {#await promise}
    <p>loading</p>
  {:then items}
    {#each items as item}
      <tr><td>{item.process}</td><td>{item.state}</td><td>{item.lag}</td><td><button type="button">{item.action}</button></td></tr>
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</table>