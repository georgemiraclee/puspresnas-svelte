<script>
    export let current_page;
    export let last_page;
    export let per_page;
    export let from;
    export let to;
    export let total;
  
    import { createEventDispatcher } from 'svelte';
  
    const dispatch = createEventDispatcher();
  
    function range(size, startAt = 0) {
      return [...Array(size).keys()].map(i => i + startAt);
    }
  
    function changePage(page) {
      if (page !== current_page) {
        dispatch('change', page);
      }
    }
  </script>
  
  <p>
    Page <code>{current_page}</code> of <code>{last_page}</code> (<code>{from + 1}</code> - <code>{to}</code> on <code>{total}</code> items)
  </p>
  
  <nav>
    <ul class="pagination">
            <li class="page-item {current_page === 1 ? 'disabled' : ''}">
                <a class="page-link" href="javascript:void(0)" on:click="{() => changePage(current_page - 1)}" rel="prev" aria-label="Kembali">&lsaquo;</a>
            </li>
  
            {#each range(last_page, 1) as page}
            <li class="page-item {page === current_page ? 'active': ''}">
                <a class="page-link" href="javascript:void(0)" on:click="{() => changePage(page)}">{page}</a>
            </li>
            {/each}
            <li class="page-item {current_page === last_page ? 'disabled' : ''}">
            <a class="page-link" href="javascript:void(0)" on:click="{() => changePage(current_page + 1)}">
                <span aria-hidden="true">»</span>
            </a>
            </li>
    </ul>
  </nav>