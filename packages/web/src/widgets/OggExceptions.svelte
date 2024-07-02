<script>
  import {
    Table,
    TableBody,
    TableBodyCell,
    TableBodyRow,
    TableHead,
    TableHeadCell,
    Checkbox,
    TableSearch,
  } from 'flowbite-svelte';
  import { onMount, onDestroy } from 'svelte';
  let promise = fetchData();

  let exceptions = [];

  async function fetchData() {
    const res = await fetch('http://10.100.18.17/bi_server/admin/json.php?module=goldengate&action=list_exceptions');
    const data = await res.json();

    if (res.ok) {
      exceptions = data;
      return data;
    } else {
      throw new Error();
    }
  }

  onMount(() => {
    const interval = setInterval(async () => {
      promise = fetchData();
    }, 60000);

    return () => clearInterval(interval);
  });
</script>

<Table>
  <TableHead>
    <TableHeadCell>Table</TableHeadCell>
    <TableHeadCell>Replicat</TableHeadCell>
    <TableHeadCell>Occurences</TableHeadCell>
  </TableHead>
  <TableBody tableBodyClass="divide-y">
    {#await promise}
      {#each exceptions as exception}
        <TableBodyRow>
          <TableBodyCell>{exception.table_name}</TableBodyCell>
          <TableBodyCell>{exception.rep_name}</TableBodyCell>
          <TableBodyCell>{exception.nbre}</TableBodyCell>
        </TableBodyRow>
      {/each}
    {:then processes}
      {#each processes as exception}
        <TableBodyRow>
          <TableBodyCell>{exception.table_name}</TableBodyCell>
          <TableBodyCell>{exception.rep_name}</TableBodyCell>
          <TableBodyCell>{exception.nbre}</TableBodyCell>
        </TableBodyRow>
      {/each}
    {:catch error}
      <p style="color: red">{error.message}</p>
    {/await}
  </TableBody>
</Table>
