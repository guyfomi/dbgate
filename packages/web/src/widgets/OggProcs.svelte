<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import LoadingInfo from '../elements/LoadingInfo.svelte';

  const dispatch = createEventDispatcher();
  let message = 'Chargement Etat Processus';

  function handleClick(process) {
    // var element = <HTMLInputElement>document.getElementById(btn.target.id);
    // element.disabled = true;
    console.debug(process);
    switch (process.id_button) {
      case 'btn_stop_capture':
        message = 'Arret processus Capture';
        promise = stopCapture();
        break;
      case 'btn_stop_propagation':
        message = 'Arret processus Propagation';
        promise = stopPropagation();
        break;
      case 'btn_stop_replication':
        message = 'Arret processus Replication';
        promise = stopReplicat();
        break;
      case 'btn_start_capture':
        message = 'Demarrage processus Capture';
        promise = startCapture();
        break;
      case 'btn_start_propagation':
        message = 'Demarrage processus Propagation';
        promise = startPropagation();
        break;
      case 'btn_start_replication':
        message = 'Demarrage processus Replication';
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
      return data;
    } else {
      throw new Error();
    }
  }

  async function startCapture() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=start_capture');
    const data = await res.json();

    if (res.ok) {
      return data;
    } else {
      throw new Error();
    }
  }

  async function stopCapture() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=stop_capture');
    const data = await res.json();

    if (res.ok) {
      return data;
    } else {
      throw new Error();
    }
  }

  async function startPropagation() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=start_propagation');
    const data = await res.json();

    if (res.ok) {
      return data;
    } else {
      throw new Error();
    }
  }

  async function stopPropagation() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=stop_propagation');
    const data = await res.json();

    if (res.ok) {
      return data;
    } else {
      throw new Error();
    }
  }

  async function startReplicat() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=start_replicat');
    const data = await res.json();

    if (res.ok) {
      return data;
    } else {
      throw new Error();
    }
  }

  async function stopReplicat() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=stop_replicat');
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
    <LoadingInfo message="message" />
  {:then processes}
    {#each processes as process}
      <tr
        ><td>{process.process}</td><td>{process.state}</td><td>{process.lag}</td><td
          ><button id={process.id_button} on:click={() => handleClick(process)} type="button">{process.action}</button
          ></td
        ></tr
      >
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</table>
