<script>
	import ThemeSelect from '$lib/theme-select.svelte'
</script>

<p class="front-sans text-2xl font-bold underline decoration-red-500 capitalize "> L'agenda des Evenements </p>

<div class="form-control">
	<input type="text" placeholder="Recherche" class="input input-bordered w-auto md:w-auto " />
</div>

<p>
	Visit <a href="https://youtu.be/yxT8bCi4u54">Damdidou</a>
</p>

<div class="chat chat-start">
	<div class="chat-bubble chat-bubble-primary">Coucou</div>
</div>
<div class="chat chat-start">
	<div class="chat-bubble chat-bubble-secondary">Je ne sais que dire</div>
</div>
<div class="chat chat-start">
	<div class="chat-bubble chat-bubble-accent">Mais je constate que cela fonctionne</div>
</div>
<div class="chat chat-end">
	<div class="chat-bubble chat-bubble-info">Calme toi Anakine.</div>
</div>
<div class="chat chat-end">
	<div class="chat-bubble chat-bubble-success">utilise la force</div>
</div>
<div class="chat chat-end">
	<div class="chat-bubble chat-bubble-warning">pour réunir la galaxie</div>
</div>
<div class="chat chat-end">
	<div class="chat-bubble chat-bubble-error">....... Et puis merde, fais ce que tu veux!</div>
</div>

<details class="collapse bg-base-200">
	<summary class="collapse-title text-xl font-medium">Clique pour voir</summary>
	<div class="collapse-content">
		<p>On te fais faire n'importe quoi!</p>
	</div>
</details>

<div class="grid grid-flow-col gap-5 text-center auto-cols-max">
	<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
    <span class="countdown font-mono text-5xl">
      <span style="--value:15;"></span>
    </span>
		days
	</div>
	<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
    <span class="countdown font-mono text-5xl">
      <span style="--value:10;"></span>
    </span>
		hours
	</div>
	<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
    <span class="countdown font-mono text-5xl">
      <span style="--value:24;"></span>
    </span>
		min
	</div>
	<div class="flex flex-col p-2 bg-neutral rounded-box text-neutral-content">
    <span class="countdown font-mono text-5xl">
      <span style="--value:41;"></span>
    </span>
		sec
	</div>
</div>



