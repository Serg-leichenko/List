<template>
  <!-- user wiew -->
  <div class="view-block">
    <div class="wiew">
      <div class="wiew__full-name bl">
        <h2 class="wiew__full-name_name">{{ user_detail.name }}</h2>
        <p class="wiew__full-name_id">
          <span>id: {{ user_detail.id }} |</span>
          <span> username: {{ user_detail.username }} |</span>
          <span> email: {{ user_detail.email }}</span>
        </p>
      </div>
      <div class="wiew__adress bl">
        <h3 class="wiew__adress_title title">Address</h3>
        <p class="wiew__adress_ad">
          {{ user_detail.address.zipcode }}
          {{ user_detail.address.street }}
          {{ user_detail.address.city }}
          {{ user_detail.address.suite }}
        </p>
        <p class="wiew__adress_geo">
          Geo:
          <span
            >Lat {{ user_detail.address.geo.lat }} Lng
            {{ user_detail.address.geo.lng }}</span
          >
        </p>
      </div>
      <div class="wiew__phone bl">
        <h3 class="wiew__phone_title title">Phone</h3>
        <p class="wiew__phone_phone">{{ user_detail.phone }}</p>
      </div>
      <div class="wiew__website bl">
        <h3 class="wiew__website_title title">Website</h3>
        <a href="#" class="wiew__website_web">{{ user_detail.website }}</a>
      </div>
      <div class="wiew__company bl">
        <h3 class="wiew__company_title title">Company</h3>
        <p class="wiew__company_text">
          {{ user_detail.company.name }}
        </p>
        <p class="wiew__company_subtext">
          {{ user_detail.company.catchPhrase }} <br />{{
            user_detail.company.bs
          }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    user_detail: Object,
    default() {
      return {};
    },
  },
};
</script>
