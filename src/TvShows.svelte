<script>
    const favorites = ['tt0903747', 'tt0116282', 'tt2356777']
    const OMDB_API = process.env.OMDB_API
    const KEY = process.env.KEY

    const fetchTvShow = async (id) => {
      const response = await fetch(`${OMDB_API}?apikey=${KEY}&i=${id}&type=series`)
      return response.json()
    }
</script>
<main>
  <div class="d-flex p-3 bd-highlight"><h5>TV Shows</h5></div>
  <div class="container">
    <div class="row">
      {#each favorites as favorite}
        
        {#await fetchTvShow(favorite)}
          <div class="col-sm">
            <p>...loading</p>
          </div>
        {:then {Title: showTitle, Plot: showDescription, Year: showYear}}
          <div class="col-sm">
            <div class="card" style="width: 18rem;">
              <div class="card-body">
                <h5 class="card-title">{showTitle}</h5>
                <p class="card-text">{showDescription}</p>
              </div>
            </div>
          </div>
        {:catch error}
          <div class="col-sm pt-3">
            <p>Ops, an error occurred fetching tv shows!</p>
          </div>
        {/await}
      {/each}
    </div>
  </div>
</main>
<style></style>