<script lang="ts">
  import { Table,Styles, Pagination, PaginationItem, PaginationLink  } from 'sveltestrap';
  import { onMount } from "svelte";
  import { Datatable } from 'svelte-simple-datatables'
    const settings = {
        sortable: true,
        pagination: true,
        scrollY: true,
        rowsPerPage: 50,
        columnFilter: false,
        css: true,
        labels: {
            search: 'Pesquisar...',    // search input placeholer
            filter: 'Filtros',       // filter inputs placeholder
            noRows: 'Nenhum registro',
            info: 'Exibir {start} de {end}. Total de registro(s):{rows}',
            previous: 'Previous',
            next: 'Next',       
        },
        blocks: {
            searchInput: true, 
            paginationButtons: true,
            paginationRowCount: true,
        }
    }    

  let rows


  let data = [];
  onMount(async function() {
    const response = await fetch("http://localhost:9000/report");
    const json = await response.json();
    data = json;
    console.log(data);
  });
</script>

<Styles />

<br><br>
<h1>REPORT</h1>

<section>
    <Datatable settings={settings} data={data} bind:dataRows={rows}>
        <thead>
            <th data-key="employment_type">Tipo</th>
            <th data-key="ethnic_group">Etnia</th>
            <th data-key="gender">Gênero</th>
            <th data-key="sexual_orientation">Orientação Sexual</th>
        </thead>
        <tbody>
        {#if rows}
            {#each $rows as row}
            <tr>
                <td>{row.employment_type}</td>
                <td>{row.ethnic_group}</td>
                <td>{row.gender}</td>
                <td>{row.sexual_orientation}</td>
            </tr>
            {/each}
        {/if}
        </tbody>
    </Datatable>
</section>

<style>
    section{width:720px;height:560px;}
    td{text-align:center;padding:4px 0}
</style>

