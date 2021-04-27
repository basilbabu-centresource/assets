<template>
  <Layout>
    <section class="single-blog">
      <div class="container">
        <div class="row">
          <div class="col-md-12 mt-40 mb-50">
            <g-image :src="getStrapiMedia($page.strapi.articles[0].image.url)" />
          </div>
          <div class="col-md-12 mb-60">
            <h2>{{ $page.strapi.articles[0].title }}</h2>
            <h6>
              {{ $page.strapi.articles[0].category.name }}
              <span>{{
                moment($page.strapi.articles[0].publishedAt).format(
                  "DD MMM YY"
                )
              }}</span>
            </h6> 
            <p>{{ $page.strapi.articles[0].content }}</p>

          </div>
        </div>
      </div>
    </section>
  </Layout>
</template>

<page-query>
query($slug: String!) {
  strapi {
    articles(where: { slug: $slug }) {
      title
      description
      content
      publishedAt
      category {
        name
      }
      image {
        url
      }
      author {
        name
        picture {
          url
        }
      }
    }
    global {
      siteName
      favicon {
        url
      }
      defaultSeo {
        metaTitle
        metaDescription
        shareImage {
          url
        }
      }
    }
  }
}
</page-query>

<script>
import VueMarkdown from "vue-markdown";
import { getStrapiMedia } from "~/utils/medias";
import { getMetaTags } from "~/utils/seo";
import moment from "moment";

export default {
  data() {
    return {
      moment: moment,
    };
  },
  components: {
    VueMarkdown,
  },
  methods: {
    getStrapiMedia,
  },
  metaInfo() {
    const { title, description, image } = this.$page.strapi.articles[0];
    const { defaultSeo, favicon } = this.$page.strapi.global;

    // Merge default and article-specific SEO data
    const seo = {
      ...defaultSeo,
      metaTitle: title,
      metaDescription: description,
      shareImage: image,
    };

    return {
      title: this.$page.strapi.articles[0].title,
      meta: getMetaTags(seo),
      link: [
        {
          rel: "favicon",
          href: getStrapiMedia(favicon.url),
        },
      ],
    };
  },
};
</script>
