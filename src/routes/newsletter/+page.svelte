<script>
  import { Label, Input, ButtonGroup, Button, Card } from "flowbite-svelte";
  import { EnvelopeSolid } from "flowbite-svelte-icons";

  const BACKEND_URL = 'https://api.lurkingryuu.tech';

	let email = '';
  const Subscribe = async () => {
	try {
	  const response = await fetch(`${BACKEND_URL}/api/subscribe`, {
		method: 'POST',
		headers: {
		  'Content-Type': 'application/json'
		},
		body: JSON.stringify({ email })
	  });
	  const data = await response.json();
	  if (response.status === 201) {
		alert('Already Subscribed');
	  } else if (response.status === 200) {
		alert('Subscribed Successfully');
	  }
	} catch (error) {
	  console.error(error);
	}
  }
</script>

<svelte:head>
  <title>News Forum</title>
  <meta name="description" content="About this app" />
</svelte:head>

<div class="text-column">
  <h1>News Letter</h1>

  <p class="mb-6 mt-6 font-bold text-gray-900 dark:text-gray-100">
    We publish our newsletter every week. Sign up to receive it — it's free, and we won't spam you! You can also unsubscribe at any time.
  </p>
  
  <Card class="w-full mx-auto md:w-1/2">
	<form class="flex flex-col space-y-6" on:submit={Subscribe}>
	  <h3 class="text-xl font-medium text-gray-900 dark:text-white">Sign in to our platform</h3>
	  <Label class="space-y-2">
		<span>Email</span>
		<Input bind:value={email} id="email" type="email" placeholder="name@example.com" required>
			<EnvelopeSolid slot="left" class="w-5 h-5 text-gray-500 dark:text-gray-400" />
		</Input>
		</Label>
	  <Button type="submit" class="w-full"
	  >
	  	Subscribe <EnvelopeSolid class="w-3.5 h-3.5 ml-2 text-white" />
	  </Button>
	</form >
  </Card>
</div>
