<script>
	import NewsCard from "/mnt/garuda/karthikeya/college/misc/devtask_svelte/src/components/NewsCard.svelte"
  import { onMount } from 'svelte';
  import axios from 'axios';

  // import dotenv from "dotenv";
  // dotenv.config();

  /** @type {string} */
  const BACKEND_URL = 'https://api.lurkingryuu.tech';

  /** @type {Array<{img: string, title: string, description: string, content: string, url: string}>} */
  let news = [];

  const getNews = async (page = 1) => {
    try {
      const response = await axios.get(`${BACKEND_URL}/api/news?page=${page}`);
      news = response.data;
    } catch (error) {
      console.error(error);
    }
  }

  onMount(async () => {
    await getNews();
  });

  // const news = [
  //   {
  //     img: "https://media.istockphoto.com/id/1463840090/photo/elephant-and-giraffe-sitting-on-a-cloud-in-the-sky-dreaming-and-aspirations-concept.webp?b=1&s=612x612&w=0&k=20&c=VLDrO8XtiLn4nAPOncGDOPLpxe3oe7H_hS6E5YSoGDk=",
  //     title: "Noteworthy technology acquisitions 2021",
  //     description: "Here are the biggest enterprise technology acquisitions of 2021 so far, in reverse chronological order.",
  //     content: "Here are the biggest enterprise technology acquisitions of 2021 so far, in reverse chronological order.",
  //     url: "https://www.cio.com/article/3620291/noteworthy-technology-acquisitions-2021.html"
  //   }
  // ]
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
	{#each news as newsItem}
    <NewsCard 
      img={newsItem.img}
      title={newsItem.title}
      description={newsItem.description}
      url={newsItem.url}
      content={newsItem.content}
    />
	{/each}
  <!-- IMplement loading and pagination -->
  <div class="flex justify-center">
    <button class="px-4 py-2 text-white bg-blue-500 rounded-md" on:click={}>Load more</button>
  </div> 
 

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
