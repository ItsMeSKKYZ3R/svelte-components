<script lang="ts">
	import Button from "../Button/Button.svelte";

	export let method: "post" | "get";
	export let action: string;
	export let classes: string = "";
	export let style: string = "";
	export let color: "dark" | "light" = "light";
</script>

<form {method} {action} class={classes} {style} id={color}>
	<slot />
</form>

<style>
	:global(form#light) {
		background-color: #ffffff;
		padding: 20px;
		padding-right: 40px;
	}

	:global(form#light label) {
		display: block;
		margin-bottom: 10px;
		font-weight: bold;
		color: #555555;
	}

	:global(form#light input[type="text"]),
	:global(form#light input[type="email"]),
	:global(form#light input[type="tel"]),
	:global(form#light textarea) {
		width: 100%;
		padding: 10px;
		border: 1px solid #dddddd;
		border-radius: 5px;
		font-size: 14px;
		color: #555555;
		margin-bottom: 20px;
	}

	:global(textarea) {
		resize: vertical;
	}

	:global(form#light button[type="submit"]) {
		color: #ffffff;
		border: none;
		padding: 10px 20px;
		border-radius: 5px;
		cursor: pointer;
		font-size: 16px;
		transition: all 0.2s ease-in-out;
	}

	:global(button[type="submit"]:hover) {
		background: #0b4efd;
	}

	:global(form#dark) {
		background-color: #333;
		padding: 20px;
		padding-right: 40px;
	}

	:global(form#dark label) {
		display: block;
		margin-bottom: 10px;
		font-weight: bold;
		color: #ccc;
	}

	:global(form#dark input),
	:global(form#dark textarea) {
		width: 100%;
		padding: 10px;
		border: 1px solid #dddddd;
		border-radius: 5px;
		font-size: 14px;
		color: #555555;
		margin-bottom: 20px;
	}

	:global(form#dark button[type="submit"]) {
		color: #ffffff;
		border: none;
		padding: 10px 20px;
		border-radius: 5px;
		cursor: pointer;
		font-size: 16px;
		transition: all 0.2s ease-in-out;
	}

	:global(button[type="submit"]:hover) {
		background: #0b4efd;
	}
</style>
