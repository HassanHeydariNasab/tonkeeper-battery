<h2>Fly with battery power</h2>
<ul class="mt-12 text-2xl">
  <li>Token swaps: ~50 charges</li>
  <li>Token transfers: ~10 charges</li>
  <li>NFT transfers: ~4 charges</li>
</ul>

<style>
  ul {
    display: grid;
    justify-items: center;
  }

  li {
    position: relative;
    display: block;
    width: fit-content;
    padding-bottom: 1em;
    opacity: 0.5;
    transition: opacity 0.2s ease-in-out;
  }

  li:hover {
    opacity: 1;
  }

  li::after {
    content: "";
    display: block;
    position: absolute;
    width: 100%;
    height: 3px;
    background: #fff;
    transition: transform 0.2s ease-in-out;
    transform: scale(0);
  }

  li:hover::after {
    transform: scale(1);
  }
</style>
