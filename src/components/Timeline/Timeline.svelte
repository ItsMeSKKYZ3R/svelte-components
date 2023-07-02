<script lang="ts">
	import { onMount } from "svelte";

	let lis: NodeListOf<Element>;

	onMount(() => {
		lis = document.querySelectorAll("ul li");

		lis.forEach((element) => {
			let childs = element.children;

			let date = childs[0];
			let title = childs[1];
			let descr = childs[2];

			date.classList.add("date");
			title.classList.add("title");
			descr.classList.add("descr");
		})
	});
</script>

<ul>
	<slot />
</ul>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap");

	:global(*,
	*::before,
	*::after) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	:global(body) {
		--color: rgba(30, 30, 30);
		--bgColor: rgba(245, 245, 245);
		min-height: 100vh;
		display: grid;
		gap: 2rem;
		font-family: "Poppins", sans-serif;
		color: var(--color);
		background: var(--bgColor);
	}

	:global(h1) {
		text-align: center;
	}

	:global(ul) {
		--col-gap: 2rem;
		--row-gap: 2rem;
		--line-w: 0.25rem;
		display: grid;
		grid-template-columns: var(--line-w) 1fr;
		grid-auto-columns: max-content;
		column-gap: var(--col-gap);
		list-style: none;
		width: min(60rem, 90%);
	}

	/* line */
	:global(ul::before) {
		content: "";
		grid-column: 1;
		grid-row: 1 / span 20;
		background: rgb(225, 225, 225);
		border-radius: calc(var(--line-w) / 2);
	}

	/* columns*/

	/* row gaps */
	:global(ul li:not(:last-child)) {
		margin-bottom: var(--row-gap);
	}

	/* card */
	:global(ul li) {
		grid-column: 2;
		--inlineP: 1.5rem;
		margin-inline: var(--inlineP);
		grid-row: span 2;
		display: grid;
		grid-template-rows: min-content min-content min-content;
	}

	/* date */
	:global(ul li .date) {
		--dateH: 3rem;
		height: var(--dateH);
		margin-inline: calc(var(--inlineP) * -1);

		text-align: center;
		background-color: var(--accent-color);

		color: white;
		font-size: 1.25rem;
		font-weight: 700;

		display: grid;
		place-content: center;
		position: relative;

		border-radius: calc(var(--dateH) / 2) 0 0 calc(var(--dateH) / 2);
	}

	/* date flap */
	:global(ul li .date::before) {
		content: "";
		width: var(--inlineP);
		aspect-ratio: 1;
		background: var(--accent-color);
		background-image: linear-gradient(rgba(0, 0, 0, 0.2) 100%, transparent);
		position: absolute;
		top: 100%;

		clip-path: polygon(0 0, 100% 0, 0 100%);
		right: 0;
	}

	/* circle */
	:global(ul li .date::after) {
		content: "";
		position: absolute;
		width: 2rem;
		aspect-ratio: 1;
		background: var(--bgColor);
		border: 0.3rem solid var(--accent-color);
		border-radius: 50%;
		top: 50%;

		transform: translate(50%, -50%);
		right: calc(100% + var(--col-gap) + var(--line-w) / 2);
	}

	/* title descr */
	:global(ul li .title,
	ul li .descr) {
		background: var(--bgColor);
		position: relative;
		padding-inline: 1.5rem;
	}
	:global(ul li .title) {
		overflow: hidden;
		padding-block-start: 1.5rem;
		padding-block-end: 1rem;
		font-weight: 500;
	}
	:global(ul li .descr) {
		padding-block-end: 1.5rem;
		font-weight: 300;
	}

	/* shadows */
	:global(ul li .title::before,
	ul li .descr::before) {
		content: "";
		position: absolute;
		width: 90%;
		height: 0.5rem;
		background: rgba(0, 0, 0, 0.5);
		left: 50%;
		border-radius: 50%;
		filter: blur(4px);
		transform: translate(-50%, 50%);
	}
	:global(ul li .title::before) {
		bottom: calc(100% + 0.125rem);
	}

	:global(ul li .descr::before) {
		z-index: -1;
		bottom: 0.25rem;
	}

	@media (min-width: 40rem) {
		:global(ul) {
			grid-template-columns: 1fr var(--line-w) 1fr;
		}
		:global(ul::before) {
			grid-column: 2;
		}
		:global(ul li:nth-child(odd)) {
			grid-column: 1;
		}
		:global(ul li:nth-child(even)) {
			grid-column: 3;
		}

		/* start second card */
		:global(ul li:nth-child(2)) {
			grid-row: 2/4;
		}

		:global(ul li:nth-child(odd) .date::before) {
			clip-path: polygon(0 0, 100% 0, 100% 100%);
			left: 0;
		}

		:global(ul li:nth-child(odd) .date::after) {
			transform: translate(-50%, -50%);
			left: calc(100% + var(--col-gap) + var(--line-w) / 2);
		}
		:global(ul li:nth-child(odd) .date) {
			border-radius: 0 calc(var(--dateH) / 2) calc(var(--dateH) / 2) 0;
		}
	}

	:global(.credits) {
		margin-top: 1rem;
		text-align: right;
	}
	:global(.credits a) {
		color: var(--color);
	}
</style>
