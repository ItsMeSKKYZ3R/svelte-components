<script lang="ts">
	export let text: string | number | boolean;
	export let type: 'button' | 'submit' | 'reset' | null | undefined = undefined;
	export let style: 'modern' | 'round';
</script>

<button {type} class={style} on:mousedown on:mouseup on:click on:dblclick on:focus on:mouseenter on:mouseleave on:mousemove on:mouseout on:mouseover on:blur>{text}</button>

<style>
	:global(button) {
		border: none;
		cursor: pointer;
		transform-origin: center;
	}

	:global(.modern) {
		background: #0d6efd;
		padding: 10px 25px;
		color: #f1f1f1;
		border-color: #0d6efd;
	}

	:global(.round) {
		background: #0d6efd;
		padding: 10px 25px;
		color: #f1f1f1;
		border-color: #0d6efd;
		border-radius: 5px;
	}
</style>
