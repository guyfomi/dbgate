<script lang="ts">
  //import { createEventDispatcher } from 'svelte';

  import LoadingInfo from '../elements/LoadingInfo.svelte';
  import { LinkedChart, LinkedLabel, LinkedValue } from 'svelte-tiny-linked-charts';
  import { onMount, onDestroy } from 'svelte';

  //const dispatch = createEventDispatcher();
  let msg = 'Chargement ...';
  let labels = [];
  let values = [];

  let promise = fetchData();

  async function fetchData() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=capture_lag');
    const result = await res.json();

    if (res.ok) {
      labels = result.labels;
      values = result.values;
      return result;
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

{#await promise}
  <LinkedChart {labels} {values} width="100%" height="100%" barMinHeight=5 grow showValue valuePrepend="Latence :" valueAppend="secondes" align="center"/>
  <!-- <LoadingInfo message={msg}/> -->
{:then}
  <LinkedChart {labels} {values} -width="100%" height="100%" barMinHeight=5 grow showValue valuePrepend="Latence :" valueAppend="secondes" align="center"/>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}