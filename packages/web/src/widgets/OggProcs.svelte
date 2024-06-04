<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { Grid, type GridColumn } from '@mediakular/gridcraft';

  // process interface
  interface Process {
    process: string;
    state: string;
    lag: number;
  }

  let columns: GridColumn<Process>[] = [
    {
      key: 'process',
      title: 'Processus',
    },
    {
      key: 'state',
      title: 'Status',
    },
    {
      key: 'lag',
      title: 'Latence',
    },    
  ];

  const dispatch = createEventDispatcher();
  let processes: Process[];

  let promise = fetchData();

  async function fetchData() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=proc_states');
    //const data = await res.json();
    processes = await res.json();

    if (res.ok) {
      return processes;
    } else {
      throw new Error();
    }
  }
</script>

<!-- <table>
  <tr><th>Processus</th><th>Status</th><th>Latence</th></tr>

  {#await promise}
    <p>loading</p>
  {:then items}
    {#each items as item}
      <tr><td>{item.process}</td><td>{item.state}</td><td>{item.lag}</td></tr>
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</table> -->

<Grid 
    bind:data={processes} 
    bind:columns />
