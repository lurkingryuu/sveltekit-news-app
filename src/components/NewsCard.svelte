<script>
  import { Card, Button } from "flowbite-svelte";
  import { ArrowRightOutline } from "flowbite-svelte-icons";

	/** @type {string} */
	export let img;

	/** @type {string} */
	export let className = "";

	/** @type {string} */
	export let url;

	/** @type {string} */
	export let title;

	/** @type {string} */
	export let description;

  /** @type {string} */
  export let content;

	
</script>

<Card
  img={img}
  class="mb-4"
>
  <h5
    class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white {className}"
  >
    {title}
  </h5>
  <p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		{description}
  </p>
  <Button href={url} target="blank" class="relative bottom-0">
    Read more <ArrowRightOutline class="w-3.5 h-3.5 ml-2 text-white" />
  </Button>
</Card>

<style>

</style>