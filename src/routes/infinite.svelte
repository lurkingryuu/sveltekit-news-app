<script>
  import { onMount } from 'svelte';
  import InfiniteScroll from 'svelte-infinite-scroll';

  /** @type {string} */
  const BACKEND_URL = 'https://api.lurkingryuu.tech';

  /** @type {Array<{img: string, title: string, description: string, content: string, url: string}>} */
  let news = [];

  const getNews = async (page = 1) => {
    try {
      const response = await fetch(`${BACKEND_URL}/api/news`);
      news = [...news, ...(await response.json())]
    } catch (error) {
      console.error(error);
    }
  }

//   let page = 1;
  onMount(async () => {
    await getNews();
  });

  /** @type {number} */
  export let page = 1;
</script>

<InfiniteScroll
    threshold={100}
    on:loadMore={async () => {
      page++;
      await getNews(page);
    }}
  />