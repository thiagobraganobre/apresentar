<script lang="ts">
  import { Table } from 'sveltestrap';
  import { onMount } from "svelte";
  let data = [];
  onMount(async function() {
    const response = await fetch("http://localhost:8080/report.json");
    const json = await response.json();
    data = json;
    console.log(data);
  });
</script>

<Table>
  <thead>
    <tr>
      <th>Tipo</th>
      <th>Gênero</th>
      <th>Etnia</th>
      <th>Sexualidade</th>
    </tr>
  </thead>
  <tbody>
      
      {#each data as record}
          <tr>
            <td>{record.employment_type}</td>
            <td>{record.gender}</td>
            <td>{record.ethnic_group}</td>
            <td>{record.sexual_orientation}</td>
          </tr>
      {/each}
  </tbody>
</Table>