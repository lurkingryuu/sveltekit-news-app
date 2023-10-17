<script>
  import { Button, Input } from "flowbite-svelte";
  import { ArrowDownOutline } from "flowbite-svelte-icons";
  import NewsCard from "../components/NewsCard.svelte";
  import { onMount } from "svelte";
  import Fuzzy from "svelte-fuzzy";
  import { PUBLIC_BACKEND_URL } from "$env/static/public";

  /** @type {string} */
  const BACKEND_URL = PUBLIC_BACKEND_URL;

  /** @type {Array<{img: String, title: String, description: String, content: String, url: String}>} */
  let data = [];

  // load data from cache
  const loadNews = () => {
    const newsCache = localStorage.getItem("news");
    if (newsCache) {
      data = JSON.parse(newsCache);
    }
  };

  // save data to cache
  const saveNews = () => {
    localStorage.setItem("news", JSON.stringify(data));
  };

  // get data from backend
  const getNews = async (page = 1) => {
    try {
      const response = await fetch(`${BACKEND_URL}/api/news?page=${page}`);
      const newsArray = await response.json();
      data = data.concat(newsArray);
      saveNews();
    } catch (error) {
      console.error(error);
    }
  };

  // refresh data in backend
  const refreshNews = async () => {
    try {
      // post to backend
      const response = await fetch(`${BACKEND_URL}/api/refresh`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
      });
    } catch (error) {
      console.error(error);
    }
  };

  let page = 1;
  onMount(async () => {
    loadNews();
    await refreshNews();
    await getNews();
  });

  const loadMore = async () => {
    page++;
    if (page % 7 === 0) {
      await refreshNews();
    }
    console.log(page);
    await getNews(page);
  };

  let query = "";

  // Fuse.js options
  // options?: { keys: string[]; [key: string]: any };
  /** @type {{ keys: string[]; [key: string]: any }} */
  let options = {
    keys: ["title"],
  };

  // { text: string; matches: boolean; key: string; }[][][]
  /** @type {Array<Array<Array<{text: string, matches: boolean, key: string}>>>} */
  let formatted = [];

  /** @type {{text: string, display: boolean}} */
  let temp = { text: "", display: false };

  /** @type {Array<{img: String, title: String, description: String, content: String, url: String}>} */
  let search_results = [];

  let searchHandler = () => {
    search_results = [];
    if (formatted.length > 0) {
      for (let i = 0; i < formatted.length; i++) {
        for (let j = 0; j < formatted[i].length; j++) {
          temp.text = "";
          temp.display = false;
          for (let k = 0; k < formatted[i][j].length; k++) {
            temp.text += formatted[i][j][k].text;
            if (formatted[i][j][k].matches) {
              temp.display = true;
            }
          }
          if (temp.display) {
            for (let l = 0; l < data.length; l++) {
              if (data[l].title === temp.text) {
                search_results.push(data[l]);
              }
            }
          }
        }
      }
      // remove duplicates
      for (let i = 0; i < search_results.length; i++) {
        for (let j = i + 1; j < search_results.length; j++) {
          if (search_results[i].url === search_results[j].url) {
            search_results.splice(j, 1);
            j--;
          }
        }
      }
      console.log(search_results);
    }
  };
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

<div class="flex justify-center mt-4 mb-4">
  <Input
    class="w-1/2"
    placeholder="Search"
    bind:value={query}
    on:input={() => {
      console.log(query);
      console.log(formatted);
      searchHandler();
    }}
  />
  <Fuzzy {query} {data} {options} bind:formatted />
</div>

<div
  class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3 justify-items-center"
>
  {#if query.length === 0}
    {#each data as newsItem}
      <NewsCard
        img={newsItem.img}
        title={newsItem.title}
        description={newsItem.description}
        url={newsItem.url}
      />
    {/each}
  {:else}
    {#each search_results as newsItem}
      <NewsCard
        img={newsItem.img}
        title={newsItem.title}
        description={newsItem.description}
        url={newsItem.url}
      />
    {/each}
  {/if}
</div>

<!-- Not found Text -->
<div 
  class="flex justify-center"
  style="display: {query.length === 0 ? 'none' : 'block'}"
>
  {#if query.length > 0}
    <h1 class="text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
      No news found
    </h1>
  {/if}
</div>  

<Button on:click={loadMore} class="mt-4 mx-auto my-auto">
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
