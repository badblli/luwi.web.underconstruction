<script setup lang="ts">
export interface SideContactProps {
  title: string
  subtitle: string
  lng: number
  lat: number
  zoom?: number
}

const props = withDefaults(defineProps<SideContactProps>(), {
  zoom: 16,
})
</script>

<template>
  <div class="side-contact">
    <div class="side-contact-inner">
      <div class="columns">
        <div class="column is-5">
          <div class="contact-card">
            <Title tag="h2" :size="5" weight="semi" narrow>
              <span>{{ props.title }}</span>
            </Title>
            <p class="paragraph mb-5">{{ props.subtitle }}</p>
            <ContactForm />
          </div>
        </div>

        <div class="column is-7">
          <div class="contact-map">
            <!-- <MapBox
              :lng="props.lng"
              :lat="props.lat"
              :zoom="props.zoom"
              absolute
            /> -->
            <iframe
              title="map"
              src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d204119.423902361!2d30.634772730026825!3d36.92942037622797!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x14c39bab9b347c63%3A0x22891f6a4c252745!2sProtalya%20Bilgi%20Teknolojileri!5e0!3m2!1str!2str!4v1690975168456!5m2!1str!2str"
              width="600"
              height="600"
              style="border: 0"
              loading="lazy"
              referrerpolicy="no-referrer-when-downgrade"
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
iframe {
  width: 100%;
  height: 100%;
}
.side-contact {
  position: relative;

  .contact-card {
    padding: 2.5rem;
    background: var(--card-bg-color);
    border: 1px solid var(--card-border-color);
    border-radius: 0.85rem;
    max-width: 440px;
    margin: 0 auto;
    transition: box-shadow 0.3s;

    &:focus-within {
      box-shadow: var(--spread-shadow);
    }
  }

  .contact-map {
    position: relative;
    width: 100%;
    height: 100%;
    min-height: 480px;
    border-radius: 0.85rem;
    overflow: hidden;
  }
}
</style>
