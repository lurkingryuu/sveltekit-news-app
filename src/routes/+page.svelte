<script>
	import { Button } from "flowbite-svelte";
  import { ArrowDownOutline } from "flowbite-svelte-icons";
  import NewsCard from "../components/NewsCard.svelte";
  import { onMount } from 'svelte';

  // import dotenv from "dotenv";
  // dotenv.config();

  /** @type {string} */
  const BACKEND_URL = 'https://api.lurkingryuu.tech';

  /** @type {Array<{img: string, title: string, description: string, content: string, url: string}>} */
  let news = [];

  const getNews = async (page = 1) => {
    try {
      const response = await fetch(`${BACKEND_URL}/api/news?page=${page}`);
      news = [...news, ...(await response.json())]
    } catch (error) {
      console.error(error);
    }
  }

  const refreshNews = async () => {
    try {
      // post to backend
      const response = await fetch(`${BACKEND_URL}/api/refresh`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        }
      });
    } catch (error) {
      console.error(error);
    }
  }

  let page = 1;
  onMount(async () => {
    await refreshNews();
    await getNews();
  });

  const loadMore = async () => {
    page++;
    if (page % 8) {
      await refreshNews();
    }
    console.log(page);
    await getNews(page);
  }
</script>

<svelte:head>
  <title>News Forum</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
  <h1>
    <span class="news-app"> News App </span>
  </h1>
</section>

<div class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3 justify-items-center">
	{#each news as newsItem}
    <NewsCard 
      img={newsItem.img}
      title={newsItem.title}
      description={newsItem.description}
      url={newsItem.url}
    />
	{/each}
</div>
<Button 
  on:click={loadMore}
  class="mt-4 mx-auto my-auto"
>
  Load more <ArrowDownOutline class="w-3.5 h-3.5 ml-2 text-white" />
</Button>

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
