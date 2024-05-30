<script>
  async function fetchData() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=proc_states');
    const data = await res.json();

    if (res.ok) {
      return data;
    } else {
      throw new Error(data);
    }
  }
</script>

<table><tr><th>Processus</th><th>Status</th><th>Latence</th></tr>

{#await fetchData()}
  <p>loading</p>
{:then items}
  {#each items as item}
  <tr><td>{item.process}</td><td>{item.state}</td><td>{item.lag}</td></tr>    
  {/each}
</table>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
