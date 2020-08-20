<style>
  .loader {
    width: 100%;
    height: 50vh;
    /* display: flex;
    align-items: center; */
    font-size: 1.5rem;
    justify-content: center;
  }
  .fas {
    display: block;
    margin-top: 2em;
    animation: spin 2000 linear 0 infinite;
  }
  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
</style>

<div class="loader flex flex-column">
  <p>Loading Your Quiz</p>
  <i class="fas fa-circle-notch" />
</div>
