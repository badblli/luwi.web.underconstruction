<route lang="yaml">
  meta:
    layout: minimal
  </route>
  
  <script setup lang="ts">
import { useSSRContext } from 'vue'

const route = useRoute()

/*
 * Here we are using the route param named "all", which is set in the file name ([...all].vue)
 * @see https://github.com/hannoeru/vite-plugin-pages#dynamic-routes
 * @see https://github.com/hannoeru/vite-plugin-pages#catch-all-routes
 */
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const slugPart = computed(() =>
  Array.isArray(route.params.all) ? route.params.all : []
)
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const slug = computed(() => `/${slugPart.value.join('/')}`)

/**
 * When the route is not found, we want to show a 404 page
 * We do this by using the `useSSRContext` composable, then we use this to set the 404 status code
 * @see src/entry-server.ts
 * @see server.ts
 */
if (import.meta.env.SSR) {
  const context = useSSRContext()

  if (context) {
    context.found = false
  }
}
</script>
  
  <template>
  <div>
    <ErrorHero color="grey" pattern>
      <template #error>
        <ErrorAnimated>
          Check back soon.
          <!-- <strong>{{ slug }}</strong> -->
        </ErrorAnimated>
      </template>
    </ErrorHero>

    <Section color="grey" wave="wave-1" shape-color="white">
      <Container>
        <SideContact
          title="Contact Us"
          subtitle="Fill out the form below to reach us"
          :lng="37.026785732927706"
          :lat="30.849006129266495"
          :zoom="16"
        />
      </Container>
    </Section>
    <footer class="footer">
      <div class="container">
        <div class="columns is-vcentered b-flex-tablet-p">
          <div class="column is-12">
            <div class="level is-mobile mobile:mb-4">
              <RouterLink
                :to="{ name: 'index' }"
                class="level-item footer-link"
              >
                <span class="icon">
                  <i class="iconify" data-icon="ion:location-outline"></i>
                </span>
                <div class="footer-text-container">
                  <p>Protalya Bilgi Teknolojileri</p>
                  <p>Göksu Mahallesi Gazi Bulvarı Karaşah İş Merkezi,</p>
                  <p>No:461 D:12, 07260 Kepez/Antalya</p>
                </div>
              </RouterLink>
            </div>
          </div>
        </div>
        <a href="tel:+908505327671" class="level-item footer-link">
          <span class="icon">
            <i class="iconify" data-icon="ion:call-outline"></i>
          </span>
          <p>08505327671</p>
        </a>
        <p class="paragraph rem-90 mt-5 footer-text has-text-centered is-6">
          <span role="img" aria-label="copyright">©</span>
          2023
          <a href="https://protalya.com">Protalya</a>
          All rights reserved.
        </p>
      </div>
    </footer>
  </div>
</template>
<style lang="scss" scoped>
footer {
  position: relative;
  padding-top: 6rem;
  padding-bottom: 3rem;
  background: var(--footer-default-bg-color);

  &.footer-overflow {
    :global(body) {
      //overflow-x: hidden;
    }
  }

  &.footer-curved {
    border-top-left-radius: 50% 20%;
    border-top-right-radius: 50% 20%;
  }

  &.footer-light {
    background: var(--footer-light-bg-color);
  }

  &.footer-dark {
    background: var(--footer-dark-bg-color);

    .title {
      color: var(--white-smoke);
      opacity: 0.6;
    }

    .footer-link {
      color: var(--white-smoke);
      opacity: 0.8;
    }

    .footer-text {
      color: var(--white-smoke);
    }
  }

  &.footer-left {
    padding-top: 3rem;
    padding-bottom: 3rem;
  }

  .footer-link {
    position: relative;
    font-family: var(--font);
    color: var(--medium-text);
    transition: color 0.3s;

    &::before {
      content: '';
      position: absolute;
      bottom: -0.5rem;
      left: 0;
      right: 0;
      margin: 0 auto;
      width: 35%;
      transform-origin: right center;
      height: 3px;
      border-radius: 50px;
      background: var(--primary);
      transform: scale(0, 1);
      transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }

    &:hover {
      color: var(--primary-light-5);
      opacity: 1;

      &::before {
        transform-origin: left center;
        transform: scale(1, 1);
      }
    }
  }

  .footer-text {
    font-family: var(--font);
    color: var(--medium-text);
  }

  .footer-logo-centered {
    display: block;
    width: 100%;

    img {
      margin: 0 auto;
    }
  }

  .footer-logo-left {
    img {
      display: block;
    }
  }
}

@media only screen and (max-width: 767px) {
  .footer-text-container {
    font-size: 12px !important;
  }

  .footer {
    .footer-link {
      margin-right: 0 !important;
    }

    &.footer-curved {
      border-top-left-radius: 80% 20%;
      border-top-right-radius: 80% 20%;
    }
  }
}

/* Add an empty line before the rule */
span.error-404 {
  display: none !important;
}
</style>