<script>
  import { onMount } from "svelte";
  import axios from "axios";
  let leagueTable = [];
  let isLoading = true;
  export let leagueCode = "PL";

  onMount(async () => {
    // https://github.com/JaxonRailey/svelte-football-standings example
    // PL = Premier League
    // BL1 = Bundesliga 1
    // SA = Serie A
    // PD = Primera Division
    // FL1 = Ligue 1
    await fetch(
      `https://api.football-data.org/v2/competitions/${leagueCode}/standings`,
      {
        headers: new Headers({
          "X-Auth-Token": import.meta.env.VITE_API_KEY,
        }),
      }
    )
      .then((response) => response.json())
      .then((data) => {
        const { standings } = data;
        // Because Svelte's reactivity is based on assignments, using array methods like .push() and .splice() won't automatically trigger updates.
        // A subsequent assignment is required to trigger the update.
        leagueTable = standings[0].table;
        console.log(leagueTable);
      })
      .catch((error) => {
        console.log(error);
        return [];
      })
      .finally(() => {
        isLoading = false;
      });
  });
</script>

<div>
  {#if !isLoading}
    <table>
      <tr>
        <th>Position</th>
        <th>Team Name</th>
        <th>Played</th>
        <th>W</th>
        <th>D</th>
        <th>L</th>
        <th>GD</th>
        <th>Points</th>
      </tr>
      {#each leagueTable as item}
        <tr>
          <td>{item.position}</td>
          <td class="flex">
            <img class="club-icon" src={item.team.crestUrl} />
            <p>{item.team.name}</p>
          </td>
          <td>{item.playedGames}</td>
          <td>{item.won}</td>
          <td>{item.draw}</td>
          <td>{item.lost}</td>
          <td>{item.goalDifference}</td>
          <td>{item.points}</td>
        </tr>
      {/each}
    </table>
  {/if}
</div>
