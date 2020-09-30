<template>
  <Layout>
    <section class="container mx-auto">
      <!-- title -->
      <h2>Sample Project: {{$page.sample.title}}</h2>
      <!-- header image -->
      <figure class="pb-8 md:pb-16">
        <picture class="block">
          <g-image
            :src="$page.sample.image"
            :alt="$page.sample.image_caption"
        /></picture>
        <figcaption class="text-xs md:text-sm text-center italic">
          {{ $page.sample.image_caption }}
        </figcaption>
      </figure>
      <!-- content -->
      <div>
        <a :href="$page.sample.git_url" target="_blank">{{$page.sample.git_url}}</a>
      </div>
      <a
          class="self-center md:self-start pb-8 md:pb-0"
          :href="'https://buildwith.ionos.com/setup?repo=' + $page.sample.git_url"
          rel="noopener"
          target="_blank"
      >
        <button
            class="text-white font-bold rounded-full bg-black inline-flex items-center shadow-lg focus:outline-none px-8 my-6 py-4"
        >
          <svg
              class="fill-current text-white w-4 h-4 mr-2"
              role="img"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
          >
            <use
                xmlns:xlink="http://www.w3.org/1999/xlink"
                xlink:href="/icons.svg#icon-ship"
            />
          </svg>
          <span>Ship to IONOS</span>
        </button>
      </a>
      <div class="markdown pb-12">
        <div v-html="$page.sample.content"></div>
      </div>
      <!-- tag cloud -->
      <ul class="flex px-16 border-t border-gray-100">
        <li class="mr-2" v-for="tag in $page.sample.tags" :key="tag.id">
          <g-link
            :to="tag.path"
            class="inline-block border border-pink-300 px-4 py-2 text-pink-500 text-xs font-semibold rounded hover:text-white hover:bg-pink-500 hover:border-pink-500"
            >{{ tag.title }}</g-link
          >
        </li>
      </ul>
    </section>
  </Layout>
</template>

<page-query>
  query($id: ID!) {
    sample(id: $id) {
      title
      path
      image
      image_caption
      excerpt
      content
      git_url
      humanTime : created(format:"Do MMMM YYYY")
      datetime : created(format:"ddd MMM DD YYYY hh:mm:ss zZ")
      author {
        name
      }
      tags {
        id
        title
        path
      }
    }
  }
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.sample.title,
    };
  },
};
</script>
