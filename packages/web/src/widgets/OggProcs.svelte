<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import LoadingInfo from '../elements/LoadingInfo.svelte';
  import { onMount, onDestroy } from 'svelte';

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
    }, 10000);

    return () => clearInterval(interval);
  });
</script>

<table>
  <tr><th>Processus</th><th>Status</th><th>Latence</th><th></th></tr>

  {#await promise}
    <!-- <LoadingInfo message={msg} /> -->
    {#each procs as process}
      <tr
        ><td style="text-align:left">{process.process}</td><td style="text-align:center">{process.state}</td><td style="text-align:center">{process.lag}</td><td
          ><button disabled id={process.id_button} on:click={() => handleClick(process)} type="button"
            >{process.action}</button
          ></td
        ></tr
      >
    {/each}
  {:then processes}
    {#each processes as process}
      <tr
        ><td style="text-align:left">{process.process}</td><td style="text-align:center">{process.state}</td><td style="text-align:center">{process.lag}</td><td
          ><button id={process.id_button} on:click={() => handleClick(process)} type="button">{process.action}</button
          ></td
        ></tr
      >
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</table>