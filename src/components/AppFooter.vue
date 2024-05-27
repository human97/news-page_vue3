<template>
  <footer class="footer">
    <div class="footer__info">
        <img alt="logo" class="footer__logo" src="@/assets/logo.svg" />
        <p class="footer__copyright">&copy; alpha, 2023</p>
    </div>
    
  </footer>
</template>

<style lang="scss" scoped>
.footer {
    display: flex;
    align-items: center;
    height: 202px;
    padding-left: 100px;
    background: #F0F6FE;

    &__logo {
        width: 114px;
        height: 36px;
    }

    &__copyright {
        font-size: 16px;
        line-height: 22.4px;
        color: #81899D;
    }
}
</style>