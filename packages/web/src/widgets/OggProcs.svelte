<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import LoadingInfo from '../elements/LoadingInfo.svelte';
  import { onMount, onDestroy } from 'svelte';
  import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from 'flowbite-svelte';

  //import { setContext, getContext } from 'svelte'

  const dispatch = createEventDispatcher();
  let msg = 'Chargement Etat Processus';
  let procs = [
    { process: 'Capture', state: '...', action: '...', id_button: 'btn_loading_capture', lag: '...' },
    { process: 'Propagation', state: '...', action: '...', id_button: 'btn_loading_propagation', lag: '...' },
    { process: 'Replication', state: '...', action: '...', id_button: 'btn_loading_replication', lag: '...' },
  ];

  function handleClick(process) {
    // var element = <HTMLInputElement>document.getElementById(btn.target.id);
    // element.disabled = true;
    console.debug(process);
    switch (process.id_button) {
      case 'btn_stop_capture':
        msg = 'Arret processus Capture';
        promise = stopCapture();
        break;
      case 'btn_stop_propagation':
        msg = 'Arret processus Propagation';
        promise = stopPropagation();
        break;
      case 'btn_stop_replication':
        msg = 'Arret processus Replication';
        promise = stopReplicat();
        break;
      case 'btn_start_capture':
        msg = 'Demarrage processus Capture';
        promise = startCapture();
        break;
      case 'btn_start_propagation':
        msg = 'Demarrage processus Propagation';
        promise = startPropagation();
        break;
      case 'btn_start_replication':
        msg = 'Demarrage processus Replication';
        promise = startReplicat();
        break;
      default:
      // code block
    }
  }

  let promise = fetchData();

  async function fetchData() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=proc_states');
    const data = await res.json();

    if (res.ok) {
      procs = data;
      return data;
    } else {
      throw new Error();
    }
  }

  async function startCapture() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=start_capture');
    const data = await res.json();

    if (res.ok) {
      procs = data;
      return data;
    } else {
      throw new Error();
    }
  }

  async function stopCapture() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=stop_capture');
    const data = await res.json();

    if (res.ok) {
      procs = data;
      return data;
    } else {
      throw new Error();
    }
  }

  async function startPropagation() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=start_propagation');
    const data = await res.json();

    if (res.ok) {
      procs = data;
      return data;
    } else {
      throw new Error();
    }
  }

  async function stopPropagation() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=stop_propagation');
    const data = await res.json();

    if (res.ok) {
      procs = data;
      return data;
    } else {
      throw new Error();
    }
  }

  async function startReplicat() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=start_replicat');
    const data = await res.json();

    if (res.ok) {
      procs = data;
      return data;
    } else {
      throw new Error();
    }
  }

  async function stopReplicat() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=stop_replicat');
    const data = await res.json();

    if (res.ok) {
      procs = data;
      return data;
    } else {
      throw new Error();
    }
  }

  onMount(() => {
    console.log('onMount');
    const interval = setInterval(async () => {
      promise = fetchData();
    }, 15000);

    return () => clearInterval(interval);
  });
</script>

<!-- <table>
  <tr><th style="text-align:left">Processus</th><th style="text-align:center">Status</th><th style="text-align:center">Latence</th></tr>

  {#await promise}    
    {#each procs as process}
      <tr
         ><td style="text-align:left">{process.process}</td><td style="text-align:center">{process.state}</td><td style="text-align:center">{process.lag}</td></tr
      >
    {/each}
  {:then processes}
    {#each processes as process}
      <tr
        ><td style="text-align:left">{process.process}</td><td style="text-align:center">{process.state}</td><td style="text-align:center">{process.lag}</td></tr 
      >
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</table> -->

<Table>
  <TableHead>
    <TableHeadCell>Processus</TableHeadCell>
    <TableHeadCell>Status</TableHeadCell>
    <TableHeadCell>Latence</TableHeadCell>    
  </TableHead>
  <TableBody tableBodyClass="divide-y">
{#await promise}    
    {#each procs as process}
    <TableBodyRow>
      <TableBodyCell>{process.process}</TableBodyCell>
      <TableBodyCell>{process.state}</TableBodyCell>
      <TableBodyCell>{process.lag}</TableBodyCell>      
    </TableBodyRow>     
    {/each}
  {:then processes}
    {#each processes as process}
    <TableBodyRow>
      <TableBodyCell>{process.process}</TableBodyCell>
      <TableBodyCell>{process.state}</TableBodyCell>
      <TableBodyCell>{process.lag}</TableBodyCell>      
    </TableBodyRow>      
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</TableBody>
</Table>