<script lang="ts">
  import { Form, FormGroup, Input, Label, Button, Toast, Styles } from 'sveltestrap';

  let isOpen = false;
  let status = 'Closed';
  const toggle = () => (isOpen = !isOpen);


  import { onMount } from "svelte";
  let data = [];
  onMount(async function() {
    const response = await fetch("http://localhost:8080/report.json");
    const json = await response.json();
    data = json;
    console.log(data);
  });
</script>

<!-- Aqui abaixo esta a chamado ao bootstrap -->
<Styles />

<h1>QUESTIONÁRIO</h1>

<Form method="post">
  <FormGroup>
    <Label for="vinculo">Qual seu tipo de vínculo</Label>
    <Input type="select" name="vinculo" id="vinculo">
      {#each data as record}
            <option>{record.employment_type}</option>
      {/each}
    </Input>
  </FormGroup>

  <FormGroup>
    <Label for="genero">Qual gênero</Label>
    <Input type="select" name="genero" id="genero">
      {#each data as record}
            <option>{record.gender}</option>
      {/each}
    </Input>
  </FormGroup>

  <FormGroup>
    <Label for="etnia">Qual etnia</Label>
    <Input type="select" name="etnia" id="etnia">
      {#each data as record}
            <option>{record.ethnic_group}</option>
      {/each}
    </Input>
  </FormGroup>

  <FormGroup>
    <Label for="sexual">Qual sua orientação sexual</Label>
    <Input type="select" name="sexual" id="sexual">
      {#each data as record}
            <option>{record.sexual_orientation}</option>
      {/each}
    </Input>
  </FormGroup>

<Button color="danger" on:click={toggle}>Enviar</Button>
<Button color="info">Apagar</Button>


</Form>





  <Toast
    body
    header="It's Toasterific"
    {isOpen}
    on:open={() => (status = 'Opened')}
    on:opening={() => (status = 'Opening...')}
    on:closing={() => (status = 'Closing...')}
    on:close={() => (status = 'Closed')}
  >
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
    quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
    consequat.
  </Toast>
