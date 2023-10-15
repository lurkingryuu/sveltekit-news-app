<script>
  import { Card, Button } from "flowbite-svelte";
  import { ArrowRightOutline } from "flowbite-svelte-icons";

	/** @type {string} */
	export let img;

	/** @type {string} */
	export let className;

	/** @type {string} */
	export let url;

	/** @type {string} */
	export let title;

	/** @type {string} */
	export let description;

	
</script>

<Card
  img={img}
  class="mb-4"
>
  <h5
    class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white {className}"
  >
    Noteworthy technology acquisitions 2021
  </h5>
  <p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
    Here are the biggest enterprise technology acquisitions of 2021 so far, in
    reverse chronological order.
  </p>
  <Button>
    Read more <ArrowRightOutline class="w-3.5 h-3.5 ml-2 text-white" />
  </Button>
</Card>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}
