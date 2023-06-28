<script lang="ts">
	import Button from "../Button/Button.svelte";

	export let method: "post" | "get";
	export let action: string;
</script>

<form {method} {action}>
	<label for="nom">Nom :</label>
	<input type="text" id="nom" name="nom" required /><br><br>

	<label for="email">Email :</label>
	<input type="email" id="email" name="email" required /><br><br>

	<label for="message">Message :</label><br>
	<textarea id="message" name="message" rows="4" cols="50" required /><br><br>

	<Button text="Envoyer" style="round" />
</form>

<style>
	form {
		background-color: #ffffff;
		padding: 20px;
		border-radius: 5px;
		padding-right: 40px;
	}

	label {
		display: block;
		margin-bottom: 10px;
		font-weight: bold;
		color: #555555;
	}

	input[type="text"],
	input[type="email"],
	textarea {
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

	:global(button[type="submit"]) {
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
