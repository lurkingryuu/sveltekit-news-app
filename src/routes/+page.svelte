<script>
  import { Card, Button } from "flowbite-svelte";
  import { ArrowRightOutline } from "flowbite-svelte-icons";
	import { NewsCard } from "/mnt/garuda/karthikeya/college/misc/devtask_svelte/src/components/NewsCard.svelte"
</script>

<svelte:head>
  <title>Home</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
  <h1>
    <span class="news-app"> News App </span>
  </h1>
</section>

<div class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3 justify-items-center">
	{#each {length: 30} as _, i}
  <Card img="https://media.istockphoto.com/id/1463840090/photo/elephant-and-giraffe-sitting-on-a-cloud-in-the-sky-dreaming-and-aspirations-concept.webp?b=1&s=612x612&w=0&k=20&c=VLDrO8XtiLn4nAPOncGDOPLpxe3oe7H_hS6E5YSoGDk=" class="mb-4">
    <h5
      class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
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
	{/each}
</div>

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

</style>
