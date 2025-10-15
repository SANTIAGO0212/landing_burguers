<template>
    <header class="header">
        <div class="header-inner">
            <div class="brand">
                <!--<img src="@/assets/logo.png" alt="logo" class="logo"/>-->
                <span class="brand-text">Burguer House</span>
            </div>
            <nav class="nav">
                <a href="#menu" class="nav-link">Menu</a>
                <a href="#about" class="nav-link">Acerca de nonosotros</a>
            </nav>
        </div>
    </header>
</template>

<style scoped>
.header {
    position: fixed;
    top:0;
    left:0;
    right: 0;
    z-index: 30;
    backdrop-filter: blur(3px);
}
.header-inner {
    max-width: 1200px;
    margin: 0 auto;
    padding: 14px 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #fff;
}
.brand {
    display: flex;
    align-items: center;
    gap: 10px;
}
.logo {
    width: 40px;
    height: 40px;
    object-fit: contain;
}
.brand-text {
    font-weight: 700;
}
.nav {
    display: flex;
    gap: 18px;
}
.nav-link {
    color: #ddd;
    text-decoration: none;
    font-weight: 500;
}
.nav-link:hover {
    color: #fff;
}
</style>