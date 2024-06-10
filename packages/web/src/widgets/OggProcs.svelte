<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  function handleClick(process) {
    // var element = <HTMLInputElement>document.getElementById(btn.target.id);
    // element.disabled = true;
    console.debug(process);
    // switch (btn.target.id) {
    //   case 'btn_stop_capture':
    //     console.log();
    //     break;
    //   case 'btn_stop_propagation':
    //     // code block
    //     break;
    //   case 'btn_stop_replication':
    //     // code block
    //     break;
    //   default:
    //   // code block
    // }
  }

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
  {:then processes}
    {#each processes as process}
      <tr
        ><td>{process.process}</td><td>{process.state}</td><td>{process.lag}</td><td
          ><button id={process.id_button} on:click={() => handleClick(process)} type="button">{process.action}</button></td
        ></tr
      >
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</table>
