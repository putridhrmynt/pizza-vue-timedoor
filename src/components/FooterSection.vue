<template>
    <footer class="footer">
        <div class="footer-content">
            <!-- Brand & Social -->
            <div class="footer-column">
                <img :src="logoAlt" alt="Logo" class="logo-img" />
                <p class="find-us">Find Us :</p>
                <div class="social-icons">
                    <div class="social-icon-wrapper">
                        <img :src="facebook" alt="Facebook" class="social-icons facebook" />
                    </div>
                    <div class="social-icon-wrapper">
                        <img :src="instagram" alt="Instagram" />
                    </div>
                    <div class="social-icon-wrapper">
                        <img :src="youtube" alt="YouTube" />
                    </div>
                </div>

            </div>

            <!-- Navigation -->
            <div class="footer-column">
                <h4 class="orange">Navigation</h4>
                <div class="nav-columns">
                    <ul>
                        <li>Home</li>
                        <li>Order</li>
                        <li>About</li>
                        <li>Blog</li>
                    </ul>
                    <ul>
                        <li>Contact</li>
                        <li>Login</li>
                        <li>Register</li>
                    </ul>
                </div>
            </div>


            <!-- Contact -->
            <div class="footer-column">
                <h4 class="orange">Contact</h4>
                <ul class="contact-list">
                    <li>
                        <img :src="email" alt="Email" class="icons" />
                        <span>Food.now@mail.com</span>
                    </li>
                    <li>
                        <img :src="phone" alt="Phone" class="icons" />
                        <span>+62848477102943</span>
                    </li>
                    <li>
                        <img :src="whatsapp" alt="WhatsApp" class="icons" />
                        <span>+628184938494</span>
                    </li>
                </ul>
            </div>


            <!-- Location -->
            <div class="footer-column">
                <h4 class="orange">Location</h4>
                <ul class="contact-list">
                    <li>
                        <img :src="location" alt="Location" class="icons" />
                        <strong>Kerobokan</strong>
                    </li>
                    
                </ul>
                <p>Jl. Raya Kerobokan Br Taman, Kuta No.98, Kerobokan Kelod, Kec. Kuta Utara, Kabupaten Badung, Bali 80361</p>
            </div>
        </div>

        <!-- Bottom -->
        <div class="footer-bottom">
            <p>Copyright © 2022 Foodnow. All Rights Reserved. Powered by PT. Timedoor Indonesia. | <a href="#">Privacy
                    Policy</a></p>
            <small>This site is protected by reCAPTCHA and the Google Privacy Policy and Terms of Service apply.</small>
        </div>
    </footer>
</template>

<script>
import logoAlt from '@/assets/logo-alt.svg';
import facebook from '@/assets/facebook.svg';
import instagram from '@/assets/instagram.svg';
import youtube from '@/assets/youtube.svg';
import email from '@/assets/mail.svg';
import phone from '@/assets/phone.svg';
import whatsapp from '@/assets/whatsapp.svg';
import location from '@/assets/location.svg';

export default {
    name: "FooterSection",
    data() {
        return {
            logoAlt,
            facebook,
            instagram,
            youtube,
            email,
            phone,
            whatsapp,
            location
        };
    }
};
</script>

<style scoped>
.footer {
    padding-top: 80px;
    color: #333;
    font-size: 14px;
}

.footer-content {
    display: flex;
    flex-wrap: wrap;
    gap: 30px;
    justify-content: space-between;
    color: #333;
}

.footer-column {
    flex: 1 1 200px;
    min-width: 200px;
}

.logo-img {
    width: 170px;
    padding-bottom: 30px;
}

.orange {
    color: #f57c00;
    font-size: 17px;
    margin-bottom: 15px;
}

.find-us {
    color: #f57c00;
    font-size: medium;
    font-weight: bold;
    font-weight: 600;
    margin-bottom: 10px;
}

.social-icons {
    display: flex;
    gap: 10px;
    align-items: center;
}

.social-icons img {
    width: 15px;
}

.facebook {
    height: 15px;
}

.social-icon-wrapper {
    width: 30px;
    height: 30px;
    border: 1px solid #f57c00;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 4px;
    transition: background-color 0.3s;
}

.social-icon-wrapper:hover {
    background-color: #F8D8BD;
}

.footer-column ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.footer-column li {
    margin-bottom: 10px;
}

.footer-column i {
    margin-right: 8px;
}

.footer-bottom {
    border-top: 1px solid #eee;
    margin-top: 30px;
    padding-top: 20px;
    text-align: center;
    font-size: 12px;
    color: #5f5f5f;
}

.footer-bottom a {
    color: #6C7881;
    text-decoration: none;
}

.footer-bottom a:hover {
    color: #f57c00;
    text-decoration: none;
}

.nav-columns {
    display: flex;
    gap: 70px;
    color: #5f5f5f;
}

.nav-columns ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.nav-columns li {
    margin-bottom: 10px;
}

.nav-columns ul li:hover {
    color: #f57c00;
    cursor: pointer;
    transition: color 0.3s ease;
}

.contact-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.contact-list li {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 8px;
}

.icons {
  width: 18px;
  height: 18px;
}
</style>