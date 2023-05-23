<script lang="ts">
  import { Alert, Form, FormGroup, Input, Label, Button, Toast, Styles } from 'sveltestrap';
  import { onMount } from "svelte";
  
  
  let TratarDadosMalditos = []; //variavel temporaria para tratamento do json em objeto
    
  let lstQuiz = [];
  let lstVinculo = [];
  let lstGenero = [];
  let lstEtnia = [];
  let lstSexualidade = [];

  onMount(async function() {
    const response = await fetch("http://localhost:9000/quiz");
    const json = await response.json();
    lstQuiz = JSON.stringify(json);
    lstQuiz = JSON.parse(lstQuiz)

    //console.log('tudao',lstQuiz);

    /* vinculo empregaticio */
    TratarDadosMalditos = lstQuiz['Qual é o seu Tipo de Vínculo com a PGE?'].options;
    for(let i = 0; i < TratarDadosMalditos.length; i++){ 
      lstVinculo[i] = {"employment_type":TratarDadosMalditos[i]};
    }

    /* genero */
    TratarDadosMalditos = lstQuiz['Com qual Gênero você se identifica'].options;
    for(let i = 0; i < TratarDadosMalditos.length; i++){ 
      lstGenero[i] = {"gender":TratarDadosMalditos[i]};
    }

    
    /* Etnia */
    TratarDadosMalditos = lstQuiz['Com qual Etnia ou cor você se identifica'].options;
    for(let i = 0; i < TratarDadosMalditos.length; i++){ 
      lstEtnia[i] = {"ethnic_group":TratarDadosMalditos[i]};
    }

    
    /* Orientacao sexual */
    TratarDadosMalditos = lstQuiz['Qual é a sua orientação sexual?'].options;
    for(let i = 0; i < TratarDadosMalditos.length; i++){ 
      lstSexualidade[i] = {"sexual_orientation":TratarDadosMalditos[i]};
    }



  });



  let vinculo = ''
	let genero = ''
	let etnia = ''
	let sexualidade = ''
	
	let respostaSalvo = ''
	async function doSave (event) {
    event.preventDefault()

    
		const res = await fetch('http://localhost:9000/quiz', {
			method: 'POST',
        redirect: 'follow',
            headers: {'Content-Type':'application/x-www-form-urlencoded'}, 
			body: 
        new URLSearchParams({
          employment_type: vinculo,
          gender: genero,
          ethnic_group: etnia,
          sexual_orientation: sexualidade
        })
		})
		
		const json = await res.json()

		respostaSalvo = JSON.stringify(json)


	}

</script>

<!-- Aqui abaixo esta a chamado ao bootstrap -->
<Styles />

<br><br>
<h1>QUIZ</h1>
{#if respostaSalvo!=""}
  <Alert color="primary" dismissible>
    <h5 class="alert-heading text-capitalize">{respostaSalvo}</h5>
  </Alert>
{/if}


<Form>
  <FormGroup>
    <Label for="vinculo"><b>Qual seu tipo de vínculo com a PGE?</b></Label>
    <Input type="select" name="employment_type" id="vinculo" bind:value={vinculo}>
      {#each lstVinculo as record}
            <option value="{record.employment_type}">{record.employment_type}</option>
      {/each}
    </Input>
  </FormGroup>

  <FormGroup>
    <Label for="genero"><b>Qual seu gênero?</b></Label>
    <Input type="select" name="gender" id="genero" bind:value={genero}>
      {#each lstGenero as record}
            <option value="{record.gender}">{record.gender}</option>
      {/each}
    </Input>
  </FormGroup>

  <FormGroup>
    <Label for="etnia"><b>Qual sua etnia?</b></Label>
    <Input type="select" name="ethnic_group" id="etnia" bind:value={etnia}>
      {#each lstEtnia as record}
            <option value="{record.ethnic_group}">{record.ethnic_group}</option>
      {/each}
    </Input>
  </FormGroup>

  <FormGroup>
    <Label for="sexual"><b>Qual sua orientação sexual?</b></Label>
    <Input type="select" name="sexual_orientation" id="sexual" bind:value={sexualidade}>
      {#each lstSexualidade as record}
            <option value="{record.sexual_orientation}">{record.sexual_orientation}</option>
      {/each}
    </Input>
  </FormGroup>

<Button color="danger" on:click={doSave}>Enviar</Button>

<Button color="info" type="reset">Apagar</Button>


</Form>
