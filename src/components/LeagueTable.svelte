<script>
  import { onMount } from "svelte";
  import axios from "axios";

  onMount(async () => {
    fetch("https://api.football-data.org/v2/competitions/BL1/standings", {
      headers: new Headers({
        "X-Auth-Token": import.meta.env.VITE_API_KEY,
      }),
    })
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
      })
      .catch((error) => {
        console.log(error);
        return [];
      });
  });
</script>

<div>
  <p>Hello world!</p>
</div>
