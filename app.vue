<template>
  <header class="header">
    <section class="header__line">
      <div class="gb-container">
        <span>FREE SHIPPING OVER $60</span>
        <span>SHOP NOW</span>
      </div>
    </section>
    <div class="header__content">
      <div class="header__container">
        <button class="header__burger">
          <img src="~/assets/icons/burger.svg" alt="" />
        </button>
        <a href="/">
          <img class="header__logo" src="~/assets/logo.svg" alt="FLUTON" />
        </a>
        <nav class="header__nav">
          <a href="/shop">
            <span>Shop</span>
            <img src="~/assets/icons/arrow.svg" alt="" />
          </a>
          <a href="/about">
            <span>About</span>
            <img src="~/assets/icons/arrow.svg" alt="" />
          </a>
          <a href="/learn">
            <span>Learn</span>
            <img src="~/assets/icons/arrow.svg" alt="" />
          </a>
        </nav>
        <button class="header__quiz">take your quiz</button>
        <button class="header__cart">
          <img src="~/assets/icons/cart.svg" alt="cart" />
        </button>
      </div>
    </div>
  </header>
  <NuxtPage />
  <footer class="footer">
    <div class="footer__item">
      <div>
        <img src="~/assets/images/fingerprint.png" alt="" />
      </div>
      <p>
        Custom molding <br />
        technology
      </p>
    </div>
    <div class="footer__item">
      <div>
        <img src="~/assets/images/cloud.png" alt="" />
      </div>
      <p>
        Supreme <br />
        comfort
      </p>
    </div>
    <div class="footer__item">
      <div>
        <img src="~/assets/images/doctor.png" alt="" />
      </div>
      <p>
        Designed by <br />
        doctors
      </p>
    </div>
    <div class="footer__item">
      <div>
        <img src="~/assets/images/earth.png" alt="" />
      </div>
      <p>
        Certified carbon <br />
        negative
      </p>
    </div>
  </footer>
</template>
<script setup lang="ts">
</script>
