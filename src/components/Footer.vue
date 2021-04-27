<template>
  <footer>
    <div class="container">
      <div class="row HO-footer-top" v-if="isHomePage">
        <div class="col-md-6">
          <h6>Newsletter</h6>
          <h2>
            Don’t see the property you were looking <br />
            for? <br />
            We will help you out by suggesting!
          </h2>
        </div>
        <div class="col-md-6 my-auto">
          <NewsletterCard @onNewsletterSubmit="NewsletterFormData($event)" />
        </div>
      </div>

      <div class="row footer-top">
        <div class="col-md-3">
          <div class="footer-about">
            <!-- <g-image src="~/assets/images/logo.png"/> -->
            <img :src="require(`../assets/images/logo.png`)" />
            <p class="mt-3 me-1">
              Asset Homez is a realization of an ambitious dream nurtured by a
              group of passionate individuals who constantly strive to put their
              best foot forward. Trustworthy in the true sense of the word, the
              immensely reputed realty expert based out of Dubai guides its
              customers to their dream abode with tremendous precision
            </p>
          </div>
        </div>
        <div class="col-md-9">
          <div class="row footer-inner-row mt-35">
            <!-- <div class="col-md-3">
                          <div class="footer-link">
                            <h3 class="mb-35">Properties</h3>
                            <ul>
                              <li><a href="#">Commercial</a></li>
                              <li><a href="#">House </a></li>
                              <li><a href="#">Office</a></li>
                              <li><a href="#">Residencial</a></li>
                              <li><a href="#">Tower</a></li>
                            </ul>
                          </div>
                        </div> -->
            <div class="col-md-3">
              <div class="footer-link">
                <h3 class="mb-25">Links</h3>
                <ul>
                  <li>
                    <g-link to="/property">Property</g-link>
                  </li>
                  <li>
                    <g-link to="/buy">Buy</g-link>
                  </li>
                  <!-- <li>
                    <g-link to="/rent">Rent</g-link>
                  </li> -->
                  <li>
                    <g-link to="/list-your-property">List Your Property</g-link>
                  </li>
                  <!-- <li>
                    <g-link to="/article">News & Blogs</g-link>
                  </li> -->
                  <li>
                    <g-link to="/about-us">About</g-link>
                  </li>
                  <li>
                    <g-link to="/careers">Careers</g-link>
                  </li>
                  <li>
                    <g-link to="/contact-us">Contact</g-link>
                  </li>
                  <li>
                    <g-link to="/privacy-policy">Privacy Policy</g-link>
                  </li>
                </ul>
              </div>
            </div>
            <div class="col-md-3">
              <div class="footer-link">
                <h3 class="mb-35">Social</h3>
                <ul>
                  <li>
                    <g-link to="https://www.facebook.com/assethomez/"> Facebook </g-link>
                  </li>
                  <li>
                    <g-link to="https://twitter.com/AssetHomez?s=09"> Twitter </g-link>
                  </li>
                  <li>
                    <g-link to="https://www.linkedin.com/company/asset-homez"> LinkedIn </g-link>
                  </li>
                  <li>
                    <g-link to="https://instagram.com/asset_homez?igshid=jwz5cq2khiob"> Instagram </g-link>
                  </li>
                  <li>
                    <g-link to="https://wa.me/+9710524563366"> Whatsapp </g-link>
                  </li>
                </ul>
              </div>
            </div>
            <div class="col-md-6">
              <div class="footer-link">
                <h3 class="mb-35">Contact Us</h3>
                <!-- <p>774 NE, Deira, Dubai</p> -->
                <p>Office 1506,&nbsp;&nbsp;Prism Tower Business Bay Dubai</p>
                <p>Post Code 19522</p>
                <p>Office: 045896555</p>
                <p>Mobile: +971 0524563366</p>
                <p>info@assethomez.com</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <div class="footer-bottom">
            <p class="mb-0 pt-15">© Copyright 2021 Asset Homez</p>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import { getMetaTags } from "~/utils/seo";
import { getStrapiMedia } from "~/utils/medias";
import { saveNewsletter } from "~/utils/custom";
import NewsletterCard from "~/components/NewsletterCard";

import { extend, ValidationObserver, ValidationProvider } from "vee-validate";
import { email, numeric, required } from "vee-validate/dist/rules";
extend("required", {
  ...required,
  message: "This field is required",
});
extend("email", {
  ...email,
  message: "Enter a valid email",
});
extend("numeric", {
  ...numeric,
  message: "Enter a valid phone number",
});

export default {
  computed: {
    isHomePage() {
      return this.$router.history.current.path === "/";
    },
  },
  name: "Footer",
  components: { ValidationProvider, ValidationObserver, NewsletterCard },
  data() {
    return {
      newsletter: { email: "" },
    };
  },
  methods: {
    saveNewsletter,
    NewsletterFormData(event) {
      this.saveNewsletter(event);
    },
  },
};
</script>
