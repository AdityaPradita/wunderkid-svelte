<script lang="ts">
  import LeagueTable from "./components/LeagueTable.svelte";
  let leagueCode = "BL1";

  const changeLeagueCode = (code) => {
    leagueCode = code;
  };
</script>

<main>
  <button on:click={() => changeLeagueCode("BL1")}>Bundesliga</button>
  <button on:click={() => changeLeagueCode("PL")}>Premier League</button>
  <button on:click={() => changeLeagueCode("SA")}>Serie A</button>
  <button on:click={() => changeLeagueCode("PD")}>La Liga</button>
  <button on:click={() => changeLeagueCode("FL1")}>Ligue 1</button>
  <LeagueTable {leagueCode} />
</main>
