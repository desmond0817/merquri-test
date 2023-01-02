<template>
  <main style="padding-top: 70px">
    <article class="media p-5">
      <figure class="media-left">
        <p class="image">
          <b-skeleton width="180px" height="180px"></b-skeleton>
        </p>
      </figure>
      <div class="media-content">
        <div class="content">
          <div v-for="i in 7" :key="i">
            <b-skeleton class="mb-1"></b-skeleton>
          </div>
        </div>
      </div>
    </article>
  </main>
</template>
