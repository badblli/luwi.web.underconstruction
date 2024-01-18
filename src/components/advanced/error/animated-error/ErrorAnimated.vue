<script setup lang="ts">
import { useDarkmode } from '/@src/stores/darkmode'
const darkmode = useDarkmode()
const src = computed(() =>
  darkmode.isDark ? '/assets/logo/LuwiLight.svg' : '/assets/logo/LuwiDark.svg'
)
</script>

<template>
  <div>
    <div class="error-nav">
      <Container>
        <div class="error-nav-inner">
          <div class="left">
            <img class="navbar-logo" :src="src" alt="logo" />
          </div>
          <div class="right">
            <ThemeToggle />
          </div>
        </div>
      </Container>
    </div>
    <div class="error-wrapper">
      <div class="error-wrapper-inner">
        <div class="underlay">
          <span class="error-404">404</span>
        </div>
        <div class="error-box">
          <div class="error-box-face front">
            <i class="iconify" data-icon="ion:construct-outline"></i>
          </div>
          <div class="error-box-face back">
            <i class="iconify" data-icon="ion:cloud-outline"></i>
          </div>
          <div class="error-box-face right">
            <i class="iconify" data-icon="ion:cog-outline"></i>
          </div>
          <div class="error-box-face left">
            <i class="iconify" data-icon="ion:hammer-outline"></i>
          </div>
          <div class="error-box-face top">
            <i class="iconify" data-icon="ion:cloud-outline"></i>
          </div>
          <div class="error-box-face bottom">
            <i class="iconify" data-icon="ion:construct-outline"></i>
          </div>
        </div>
        <div class="error-box-shadow"></div>
      </div>
      <div class="error-content">
        <Title tag="h2" :size="2" weight="semi" narrow>
          <!-- <span>Page Not Found</span> -->
          <span>The Under Construction</span>
        </Title>
        <Title tag="h2" :size="5" weight="thin">
          <slot>
            Oops, something went wrong and we couldn't find that page. Please
            try again later.
          </slot>
        </Title>
        <Buttons alignment="centered">
          <!-- <Button to="/" :long="3" color="light" outlined bold>Homepage</Button>
          <Button
            :long="3"
            color="light"
            outlined
            bold
            @click.prevent="$router.back()"
            @keydown.space.prevent="() => $router.back()"
          >
            Back
          </Button> -->
          <Button
            icon-left="feather:instagram"
            href="https://www.instagram.com/protalya_/"
            :long="3"
            outlined
            bold
          >
            Instagram
          </Button>
        </Buttons>
        <Title tag="h2" :size="2" weight="bold" inverted leading>
          <!-- <span>Page Not Found</span> -->
          <i class="iconify" data-icon="ion:chevron-down-outline"></i>
        </Title>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
span.error-404 {
  display: none !important;
}

.error-nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 3;

  .error-nav-inner {
    height: 4rem;
    display: flex;
    align-items: center;
    justify-content: space-between;

    .left {
      display: flex;
      align-items: center;

      .navbar-logo {
        min-height: 40px;
        max-height: 65px;
        // filter: brightness(0) invert(1);
      }
    }

    .right {
      display: flex;
      align-items: center;
      justify-content: flex-end;
    }
  }
}

.error-wrapper {
  position: relative;
  top: 2rem;
  overflow: hidden;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  padding: 3rem 0;

  .error-wrapper-inner {
    position: relative;
    perspective: 400px;

    .underlay {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-family: var(--font);
      font-weight: 900;
      font-size: 25rem;
      color: var(--white-smoke);
      opacity: 0.1;
      z-index: 0;
    }
  }

  .error-box {
    position: relative;
    width: 200px;
    height: 200px;
    font-family: var(--font);
    transform-style: preserve-3d;
    transform: translateZ(-100px);
    transition: 0.3s;
    animation-name: rotateAnimation;
    animation-duration: 4s;
    animation-iteration-count: infinite;

    .error-box-face {
      position: absolute;
      width: 200px;
      height: 200px;
      font-size: 120px;
      line-height: 200px;
      text-align: center;
      color: var(--white);
      border: 1px solid bix#000;

      &.front {
        transform: rotateY(0deg) translateZ(100px);
        background: #20162b;
      }

      &.back {
        transform: rotateY(90deg) translateZ(100px);
        background: darken(#20162b, 5%);
      }

      &.right {
        transform: rotateY(180deg) translateZ(100px);
        background: darken(#20162b, 10%);
      }

      &.left {
        transform: rotateY(-90deg) translateZ(100px);
        background: darken(#20162b, 15%);
      }

      &.top {
        transform: rotateX(90deg) translateZ(100px);
        background: darken(#20162b, 5%);
      }

      &.bottom {
        transform: rotateX(-90deg) translateZ(100px);
        background: darken(#20162b, 20%);
      }
    }
  }

  @keyframes rotateAnimation {
    25% {
      transform: translateZ(-100px) rotateY(-90deg);
    }

    50% {
      transform: translateZ(-100px) rotateY(-180deg);
    }

    75% {
      transform: translateZ(-100px) rotateX(-90deg);
    }

    85% {
      transform: translateZ(-100px) rotateX(-90deg);
    }
  }

  .error-box-shadow {
    position: absolute;
    z-index: -1;
    left: -50px;
    top: calc(100% - 20px);
    width: calc(100% + 100px);
    height: 30px;
    border-radius: 50%;
    background: #000;
    filter: blur(20px);
  }

  .error-content {
    margin-top: 4rem;
    text-align: center;
  }
}

@media only screen and (max-width: 767px) {
  .error-nav {
    .error-nav-inner {
      padding: 0 1rem;
    }
  }

  .error-wrapper {
    :deep(.title) {
      font-size: 2rem;
    }

    .paragraph {
      font-size: 1rem !important;
    }

    .error-wrapper-inner {
      .underlay {
        font-size: 12rem;
      }
    }
  }
}

@media only screen and (min-width: 768px) and (max-width: 1024px) and (orientation: portrait) {
  .error-nav {
    .error-nav-inner {
      padding: 0 1rem;
    }
  }
}
</style>
