<script lang="ts">
	import Button from "../Button/Button.svelte";

	export let method: "post" | "get";
	export let action: string;
	export let classes: string = "";
	export let style: string = "";
	export let color: "dark" | "light" = "light";
</script>

<form {method} {action} class={classes} {style} id={color}>
	<label for="nom">Nom :</label>
	<input type="text" id="nom" name="nom" required /><br><br>

	<label for="email">Email :</label>
	<input type="email" id="email" name="email" required /><br><br>

	<label for="message">Message :</label><br>
	<textarea id="message" name="message" rows="4" cols="50" required /><br><br>

	<Button text="Envoyer" style="round" />
</form>

<style>
	form#light {
		background-color: #ffffff;
		padding: 20px;
		border-radius: 5px;
		padding-right: 40px;
	}

	form#light label {
		display: block;
		margin-bottom: 10px;
		font-weight: bold;
		color: #555555;
	}

	form#light input[type="text"],
	form#light input[type="email"],
	form#light textarea {
		width: 100%;
		padding: 10px;
		border: 1px solid #dddddd;
		border-radius: 5px;
		font-size: 14px;
		color: #555555;
		margin-bottom: 20px;
	}

	textarea {
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

	/* */

	form#dark {
		background-color: #333;
		padding: 20px;
		border-radius: 5px;
		padding-right: 40px;
	}

	form#dark label {
		display: block;
		margin-bottom: 10px;
		font-weight: bold;
		color: #ccc;
	}

	form#dark input[type="text"],
	form#dark input[type="email"],
	form#dark textarea {
		width: 100%;
		padding: 10px;
		border: 1px solid #dddddd;
		border-radius: 5px;
		font-size: 14px;
		color: #555555;
		margin-bottom: 20px;
	}

	textarea {
		resize: vertical;
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
