<template>
  <section class="hero">
    <!-- Header/Navbar -->
    <header class="navbar">
      <div>
        <img :src="logo" alt="Logo" class="logo-img" />
      </div>
      <nav class="nav-links">
        <a href="#">Home</a>
        <a href="#">Order</a>
        <a href="#">About</a>
        <a href="#">Blog</a>
        <a href="#">Contact us</a>
      </nav>
      <div class="auth-buttons">
        <a href="#" class="login">Login</a>
        <a href="#" class="register">Register</a>
      </div>
    </header>

    <!-- Hero Title -->
    <div class="overlay">
      <h1 class="hero-title">Pizza order</h1>
    </div>
  </section>
</template>

<script>
import logo from '@/assets/logo.svg';

export default {
  name: "HeroSection",
  data() {
    return {
      logo
    };
  }
};
</script>


<style scoped>
.hero {
  background-image: url('@/assets/hero.png');
  background-size: cover;
  background-position: center;
  height: 500px;
  position: relative;
}

.overlay {
  background-color: rgba(0, 0, 0, 0.1);
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* === Header/Navbar === */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 90px;
  position: absolute;
  width: 100%;
  z-index: 10;
  font-size: small;
  font-weight: bold;
}

.logo-img {
  height: 25px;
}

.nav-links a {
  margin: 0 1rem;
  color: white;
  text-decoration: none;
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: #f57c00;
}

.auth-buttons {
  display: flex;
  gap: 15px;
  align-items: center;
}

.login {
  color: white;
  text-decoration: none;
  transition: color 0.3s ease;
}

.login:hover {
  color: #f57c00;
}

.register {
  padding: 0.5rem 1rem;
  background-color: #f57c00;
  border-radius: 20px;
  color: white;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.register:hover {
  background-color: #C16515;
}

/* === Hero Title === */
.hero-title {
  font-size: 4rem;
  font-weight: bold;
  color: #f57c00;
}
</style>
