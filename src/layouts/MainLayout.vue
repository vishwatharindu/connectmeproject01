<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-white text-dark" height-hint="64">
      <q-toolbar style="height: 64px">
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          aria-label="Menu"
          icon="menu"
          class="lt-md"
        />

        <q-toolbar-title shrink class="row items-center no-wrap q-mr-md">
          <q-avatar color="primary" text-color="white" icon="hub" size="sm" class="q-mr-sm" />
          <span class="text-weight-bold">[PlatformName]</span>
        </q-toolbar-title>

        <q-space />

        <q-tabs
          v-model="navTab"
          shrink
          stretch
          dense
          align="left"
          class="gt-sm"
          active-color="primary"
        >
          <q-route-tab name="home" label="Home" to="/" exact no-caps />
          <q-route-tab name="features" label="Features" to="/#features" no-caps />
          <q-route-tab name="marketplace" label="Marketplace" to="/marketplace" no-caps />
          <q-route-tab name="experts" label="Experts" to="/consultants" no-caps />
          <q-route-tab name="community" label="Community" to="/community" no-caps />
        </q-tabs>

        <q-space />

        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn outline dense color="primary" label="Log In" to="/login" no-caps padding="xs md" />
          <q-btn
            unelevated
            dense
            color="primary"
            label="Sign Up"
            to="/register"
            no-caps
            padding="xs md"
          />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered class="bg-grey-1" :width="240">
      <q-scroll-area class="fit">
        <q-list padding>
          <q-item-label header class="text-grey-8">Navigation</q-item-label>
          <q-item clickable v-ripple to="/" exact
            ><q-item-section avatar><q-icon name="home" /></q-item-section
            ><q-item-section>Home</q-item-section></q-item
          >
          <q-item clickable v-ripple to="/marketplace"
            ><q-item-section avatar><q-icon name="storefront" /></q-item-section
            ><q-item-section>Marketplace</q-item-section></q-item
          >
          <q-item clickable v-ripple to="/services"
            ><q-item-section avatar><q-icon name="local_mall" /></q-item-section
            ><q-item-section>Services</q-item-section></q-item
          >
          <q-item clickable v-ripple to="/consultants"
            ><q-item-section avatar><q-icon name="groups" /></q-item-section
            ><q-item-section>Experts</q-item-section></q-item
          >
          <q-item clickable v-ripple to="/community"
            ><q-item-section avatar><q-icon name="forum" /></q-item-section
            ><q-item-section>Community</q-item-section></q-item
          >
          <q-separator class="q-my-md" />
          <q-item clickable v-ripple to="/dashboard" v-if="isUserLoggedIn"
            ><q-item-section avatar><q-icon name="dashboard" /></q-item-section
            ><q-item-section>Dashboard</q-item-section></q-item
          >
          <q-item clickable v-ripple to="/settings" v-if="isUserLoggedIn"
            ><q-item-section avatar><q-icon name="settings" /></q-item-section
            ><q-item-section>Settings</q-item-section></q-item
          >
          <q-item clickable v-ripple @click="logout" v-if="isUserLoggedIn"
            ><q-item-section avatar><q-icon name="logout" /></q-item-section
            ><q-item-section>Logout</q-item-section></q-item
          >
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer bordered class="bg-grey-10 text-grey-5">
      <div class="container q-py-xl">
        __
        <div class="row q-col-gutter-lg">
          <div class="col-12 col-sm-6 col-md-3">
            <div class="text-subtitle1 text-weight-bold text-white q-mb-md">Categories</div>
            <q-list dense>
              <q-item
                clickable
                dense
                class="q-pa-none q-mb-xs"
                v-for="cat in categories"
                :key="cat.label"
                :to="cat.link"
              >
                <q-item-section class="text-grey-5 hover-white">{{ cat.label }}</q-item-section>
              </q-item>
            </q-list>
          </div>

          <div class="col-12 col-sm-6 col-md-3">
            <div class="text-subtitle1 text-weight-bold text-white q-mb-md">For Clients</div>
            <q-list dense>
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/how-to-hire"
                ><q-item-section class="text-grey-5 hover-white"
                  >How to Hire</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/post-project"
                ><q-item-section class="text-grey-5 hover-white"
                  >Post a Project</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/services"
                ><q-item-section class="text-grey-5 hover-white"
                  >Browse Services</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/consultants"
                ><q-item-section class="text-grey-5 hover-white"
                  >Find Consultants</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/trust-safety"
                ><q-item-section class="text-grey-5 hover-white"
                  >Trust & Safety</q-item-section
                ></q-item
              >
            </q-list>
          </div>

          <div class="col-12 col-sm-6 col-md-3">
            <div class="text-subtitle1 text-weight-bold text-white q-mb-md">For Professionals</div>
            <q-list dense>
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/how-to-work"
                ><q-item-section class="text-grey-5 hover-white"
                  >How it Works</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/create-profile"
                ><q-item-section class="text-grey-5 hover-white"
                  >Create Profile</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/offer-services"
                ><q-item-section class="text-grey-5 hover-white"
                  >Offer Services</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/become-consultant"
                ><q-item-section class="text-grey-5 hover-white"
                  >Become a Consultant</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/community"
                ><q-item-section class="text-grey-5 hover-white"
                  >Community Hub</q-item-section
                ></q-item
              >
            </q-list>
          </div>

          <div class="col-12 col-sm-6 col-md-3">
            <div class="text-subtitle1 text-weight-bold text-white q-mb-md">Company</div>
            <q-list dense>
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/about"
                ><q-item-section class="text-grey-5 hover-white">About Us</q-item-section></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/careers"
                ><q-item-section class="text-grey-5 hover-white">Careers</q-item-section></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/press"
                ><q-item-section class="text-grey-5 hover-white"
                  >Press & News</q-item-section
                ></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/blog"
                ><q-item-section class="text-grey-5 hover-white">Blog</q-item-section></q-item
              >
              <q-item clickable dense class="q-pa-none q-mb-xs" to="/contact"
                ><q-item-section class="text-grey-5 hover-white">Contact Us</q-item-section></q-item
              >
            </q-list>
          </div>
        </div>
      </div>

      <q-separator dark spaced />

      <q-toolbar class="container">
        __
        <div class="row items-center justify-between full-width">
          <div class="text-caption">
            <span class="text-weight-bold">[PlatformName]</span> &copy; {{ currentYear }} All rights
            reserved.
          </div>

          <div class="q-gutter-sm">
            <q-btn flat round dense type="a" href="#" target="_blank" aria-label="Twitter">
              <q-icon name="lab la-twitter" /> __
            </q-btn>
            <q-btn flat round dense type="a" href="#" target="_blank" aria-label="Facebook">
              <q-icon name="lab la-facebook-f" />
            </q-btn>
            <q-btn flat round dense type="a" href="#" target="_blank" aria-label="LinkedIn">
              <q-icon name="lab la-linkedin-in" />
            </q-btn>
            <q-btn flat round dense type="a" href="#" target="_blank" aria-label="Instagram">
              <q-icon name="lab la-instagram" />
            </q-btn>
          </div>
        </div>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { ref, computed } from 'vue' // Import computed

const leftDrawerOpen = ref(false)
const navTab = ref('home')
const isUserLoggedIn = ref(false) // Placeholder

// Categories for Footer (Example - Replace with your actual categories)
const categories = ref([
  { label: 'Graphics & Design', link: '/categories/graphics-design' },
  { label: 'Digital Marketing', link: '/categories/digital-marketing' },
  { label: 'Writing & Translation', link: '/categories/writing-translation' },
  { label: 'Video & Animation', link: '/categories/video-animation' },
  { label: 'Music & Audio', link: '/categories/music-audio' },
  { label: 'Programming & Tech', link: '/categories/programming-tech' },
  { label: 'Consulting', link: '/categories/consulting' },
  // Add more categories
])

// Get current year for copyright
const currentYear = computed(() => new Date().getFullYear())

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function logout() {
  console.log('User logout')
  isUserLoggedIn.value = false
}
</script>

<style scoped>
.q-footer {
  /* Optional: add min-height or specific styles */
}
.q-toolbar {
  min-height: 48px; /* Consistent height */
}
.hover-white:hover {
  color: rgb(139, 133, 133) !important; /* Override default link hover if needed */
}
.q-item {
  min-height: 32px; /* Adjust density */
}
.q-item__section {
  padding-right: 8px; /* Adjust spacing */
}

/* Ensure Line Awesome icons are available if you use them */
/* You might need to add Line Awesome via quasar.config.js extras or CDN */
</style>
