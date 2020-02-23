<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.8.0/css/bulma.min.css">
</svelte:head>
<div class='hero is-fullheight is-info'>
	<div class='hero-body'>
		<div class='container has-text-centered is-fluid'>
		<div class='columns'>
		<div class='column is-one-third is-offset-one-third'>
			<h1 class='title'>#b2d</h1>
			<h2 class='subtitle'>binary to decimal converter</h2>
		<section class='section is-medium'>
			<h2 class='subtitle'>Choose your binary size in bytes (1 byte = 8 bits)</h2>
			<input class='input is-fullwidth is-large has-text-centered' type='number' bind:value={size} min="1">
		</section>
			<section class='section is-medium'>
   			<h2 class='subtitle'>... type the binary here</h2>
				<input bind:value={binary} class='input is-fullwidth is-large has-text-centered' maxlength={maxlength}
				 placeholder='type the binary here' on:keydown={onKeydownHandler} />
			</section>
			<section class='section is-medium'>
				<h2 class='subtitle'>.. and get the decimal number here</h2>
				<input value={decimal} class='input is-static has-text-white is-fullwidth is-large is-danger has-text-centered'
				 readonly />
			</section>
			{#if error}
			<div class='notification is-warning has-text-centered'>
				<button class="delete" on:click={onClickHandler}></button>
				{error}
			</div>
			{/if}
		</div>
		</div>
	</div>
	</div>
</div>
<script>
  let binary = "";
	let error = "";
	let size = 1;
	$: decimal = parseInt(binary || "0", 2);
	$: maxlength = size * 8

  const onClickHandler = () => {
    error = "";
  };

  const onKeydownHandler = event => {
    const { keyCode, key } = event;
    if (![8, 48, 49, 46, 37, 39, 96, 97].find(k => k === keyCode)) {
      error = `Invalid key ${key} pressed`;
      event.preventDefault();
      return;
    }
    error = "";
  };
</script>
<style>
	.notification {
	  position: fixed;
	  top: 5px;
	  left: 25%;
	  width: 50%;
	}
	.section { 
		padding: 1rem;
	}
</style> 