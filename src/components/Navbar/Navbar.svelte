<script lang="ts">
	import { onMount } from "svelte";

    export let websiteName: string;
    export let navbarLogo: string | null = null;

	let navbarToggle: Element | null;
	let isNavbarExpanded: string | boolean;
    let li: NodeListOf<Element>;
    let a: NodeListOf<Element>;

	onMount(() => {
		navbarToggle = document.querySelector("#navbar-toggle");

		if (navbarToggle) {
			isNavbarExpanded = navbarToggle.getAttribute("aria-expanded") === "true";
		}

		const toggleNavbarVisibility = () => {
			if (navbarToggle) {
				isNavbarExpanded = !isNavbarExpanded;
				navbarToggle.setAttribute("aria-expanded", `${isNavbarExpanded}`);
			}
		};

		if (navbarToggle) {
			navbarToggle.addEventListener("click", toggleNavbarVisibility);
		}

        li = document.querySelectorAll(".navbar-links li");

        li?.forEach((liItem) => {
            liItem?.classList.add("navbar-item");
        })

        a = document.querySelectorAll(".navbar-links li a");

        a.forEach((aItem) => {
            aItem?.classList.add("navbar-link");
        })
	});
</script>

<head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
	/>
</head>
<!-- svelte-ignore a11y-invalid-attribute -->
<header id="navbar">
	<nav class="navbar-container container">
		<a href="/" class="home-link">
			<div class="navbar-logo" />
            {#if navbarLogo !== null}
                <img src={navbarLogo} alt="Navbar Logo" class="navbar-logo">
            {/if}
			{websiteName}
		</a>
		<button type="button" id="navbar-toggle" aria-controls="navbar-menu" aria-label="Toggle menu" aria-expanded="false">
			<span class="icon-bar" />
			<span class="icon-bar" />
			<span class="icon-bar" />
		</button>
		<div id="navbar-menu" aria-labelledby="navbar-toggle">
			<ul class="navbar-links">
                <slot />
			</ul>
		</div>
	</nav>
</header>

<style>
	:global(:root) {
		--navbar-bg-color: hsl(0, 0%, 15%);
		--navbar-text-color: hsl(0, 0%, 85%);
		--navbar-text-color-focus: white;
		--navbar-bg-contrast: hsl(0, 0%, 25%);
	}

	:global(.container) {
		max-width: 1000px;
		padding: 0 1.4rem;
		margin: 0 auto;
	}

	:global(#navbar) {
		--navbar-height: 64px;
		position: fixed;
		height: var(--navbar-height);
		background-color: var(--navbar-bg-color);
		left: 0;
		right: 0;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.15);
	}

	:global(.navbar-container) {
		display: flex;
		justify-content: space-between;
		height: 100%;
		align-items: center;
	}

	:global(.navbar-item) {
		margin: 0.4em;
		width: 100%;
	}

	:global(.home-link,
	.navbar-link) {
		color: var(--navbar-text-color);
		text-decoration: none;
		display: flex;
		font-weight: 400;
		align-items: center;
	}

	:global(.home-link:is(:focus, :hover)) {
		color: var(--navbar-text-color-focus);
	}

	:global(.navbar-link) {
		justify-content: center;
		width: 100%;
		padding: 0.4em 0.8em;
		border-radius: 5px;
	}

	:global(.navbar-link:is(:focus, :hover)) {
		color: var(--navbar-text-color-focus);
		background-color: var(--navbar-bg-contrast);
	}

	:global(.navbar-logo) {
		border-radius: 50%;
		width: 30px;
		height: 30px;
		margin-inline-start: 0.5em;
	}

	:global(#navbar-toggle) {
		cursor: pointer;
		border: none;
		background-color: transparent;
		width: 40px;
		height: 40px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

	:global(.icon-bar) {
		display: block;
		width: 25px;
		height: 4px;
		margin: 2px;
		background-color: var(--navbar-text-color);
	}

	:global(#navbar-toggle:is(:focus, :hover) .icon-bar) {
		background-color: var(--navbar-text-color-focus);
	}

	:global(#navbar-toggle[aria-expanded="true"] .icon-bar:is(:first-child, :last-child)) {
		position: absolute;
		margin: 0;
		width: 30px;
	}

	:global(#navbar-toggle[aria-expanded="true"] .icon-bar:first-child) {
		transform: rotate(45deg);
	}

	:global(#navbar-toggle[aria-expanded="true"] .icon-bar:nth-child(2)) {
		opacity: 0;
	}

	:global(#navbar-toggle[aria-expanded="true"] .icon-bar:last-child) {
		transform: rotate(-45deg);
	}

	:global(#navbar-menu) {
		position: fixed;
		top: var(--navbar-height);
		bottom: 0;
		opacity: 0;
		visibility: hidden;
		left: 0;
		right: 0;
	}

	:global(#navbar-toggle[aria-expanded="true"] + #navbar-menu) {
		background-color: rgba(0, 0, 0, 0.4);
		opacity: 1;
		visibility: visible;
        transition: all 0.5 ease-in-out;
	}

	:global(.navbar-links) {
		list-style: none;
		position: absolute;
		background-color: var(--navbar-bg-color);
		display: flex;
		flex-direction: column;
		align-items: center;
		left: 0;
		right: 0;
		margin: 1.4rem;
		border-radius: 5px;
		box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
	}

	:global(#navbar-toggle[aria-expanded="true"] + #navbar-menu .navbar-links) {
		padding: 1em;
	}
</style>