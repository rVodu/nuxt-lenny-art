<template>
  <div class="home">
    <AppHero class="home__hero" />

    <section id="events">
      <AppOffers class="home__offers" />
    </section>

    <section id="about">
      <AppAbout class="home__about" />
    </section>

    <AppUpcoming class="home__upcoming" />

    <section id="blog">
      <AppListing v-slot="{ list }" title="Блог" :moreLink="true" :grid="'column'"
        :url="'http://localhost:3000/json/blog.json'" class="home__listing">
        <ArticleCard v-for="card in list" :key="card.slug" :data="card" class="app-listing__card" />
      </AppListing>
    </section>

    <section id="contacts">
      <AppContacts class="home__contacts" />
    </section>

    <AppDoit class="home__doit" />
  </div>
</template>


<script setup>

const list = ref([]);
const URL = "http://localhost:3000/json/events.json";

const { data } = await useAsyncData(`events`, () => {
  return $fetch(URL);
});
if (data?.value) list.value = data.value;

</script>

<style lang="less">
.home {
  width: 100%;
  margin-top: 100px;
  margin-bottom: 200px;

  @media @bw1370 {
    margin-bottom: 100px;
  }

  @media @bw768 {
    margin-bottom: 40px;
    margin-top: 80px;
  }
}

#events,
#blog,
#about,
#contacts {
  scroll-margin-top: 170px;
}
</style>