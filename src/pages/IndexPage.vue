<template>
  <q-page padding class="bg-slate-50">
    <div
      class="hero-section text-center q-py-xl q-px-md bg-gradient-primary text-white rounded-borders q-mb-xl shadow-4 overflow-hidden position-relative"
    >
      <div class="floating-shapes">
        <div v-for="n in 6" :key="`shape-${n}`" class="floating-shape" :class="`shape-${n}`"></div>
      </div>

      <h1 class="text-h2 text-weight-bold q-mb-md animate-fade-in" style="line-height: 1.2">
        ඔබේ වෘත්තීය ඉලක්ක ජයගන්න!
      </h1>
      <p
        class="text-h6 text-blue-1 q-mb-lg animate-fade-in-delay-1"
        style="max-width: 800px; margin: auto; opacity: 0.9"
      >
        විශිෂ්ට Freelancers, සේවා සහ උපදේශකයින් සොයාගන්න. ක්‍රියාකාරී ප්‍රජාවට එක්වන්න.
      </p>
      <div class="q-mx-auto animate-fade-in-delay-2" style="max-width: 650px">
        <q-input
          v-model="searchQuery"
          placeholder="කුසලතාවක්, සේවාවක් හෝ වෘත්තිකයෙක් සොයන්න..."
          outlined
          rounded
          dense
          bg-color="white"
          class="q-mb-sm custom-search-input shadow-2"
          input-class="text-dark"
          input-style="padding: 10px 15px;"
          @focus="searchFocused = true"
          @blur="searchFocused = false"
          :class="{ 'search-focused': searchFocused }"
        >
          <template v-slot:append>
            <q-btn
              unelevated
              rounded
              color="amber"
              text-color="dark"
              label="සොයන්න"
              icon-right="search"
              no-caps
              padding="sm lg"
              @click="performSearch"
              class="q-ml-sm search-btn"
            />
          </template>
        </q-input>
        <div class="text-blue-2 text-caption q-mt-sm">
          <q-icon name="verified_user" size="xs" class="q-mr-xs" />
          Trusted by 10,000+ Professionals & Businesses
        </div>
      </div>
    </div>

    <section id="features" class="q-mb-xl q-mt-xl">
      <h2 class="text-h4 text-weight-medium text-center text-slate-800 q-mb-xl section-title">
        අපගේ ප්‍රධාන සේවාවන්
      </h2>
      <transition-group appear tag="div" class="row q-col-gutter-xl" name="feature-anim">
        <div
          class="col-12 col-sm-6 col-lg-3"
          v-for="(feature, index) in features"
          :key="feature.title"
          :style="`--feature-index: ${index}`"
        >
          <q-intersection once transition="scale">
            <q-card
              flat
              class="feature-card text-center q-pa-lg full-height bg-white rounded-borders"
              style="border: 1px solid var(--q-color-grey-3)"
            >
              <q-card-section class="q-pt-none">
                <q-avatar
                  size="64px"
                  :icon="feature.icon"
                  :color="feature.color + '-1'"
                  :text-color="feature.color + '-7'"
                  class="q-mb-md pulse-avatar"
                />
                <div class="text-h6 text-weight-medium text-slate-800 q-mb-sm">
                  {{ feature.title }}
                </div>
                <p class="text-body2 text-slate-600">{{ feature.description }}</p>
              </q-card-section>
              <q-card-actions align="center" class="absolute-bottom q-pb-md">
                <q-btn
                  flat
                  :color="feature.color + '-7'"
                  :label="feature.btnLabel"
                  no-caps
                  icon-right="arrow_forward"
                  :to="feature.link"
                  class="text-weight-medium btn-hover-effect"
                />
              </q-card-actions>
            </q-card>
          </q-intersection>
        </div>
      </transition-group>
    </section>

    <section id="marketplace" class="q-mb-xl q-mt-xl">
      <q-intersection once transition="slide-right">
        <h2 class="text-h4 text-weight-medium text-center text-slate-800 q-mb-lg section-title">
          Featured Services & Talent
        </h2>
      </q-intersection>
      <q-tabs
        v-model="marketplaceTab"
        dense
        class="text-grey-7 q-mb-lg custom-tabs"
        active-color="primary"
        indicator-color="primary"
        align="left"
        narrow-indicator
        active-bg-color="blue-1"
        style="border-radius: 8px; border: 1px solid var(--q-color-grey-3)"
      >
        <q-tab
          name="services"
          label="Featured Services"
          no-caps
          style="border-right: 1px solid var(--q-color-grey-3)"
        />
        <q-tab
          name="freelancers"
          label="Top Freelancers"
          no-caps
          style="border-right: 1px solid var(--q-color-grey-3)"
        />
        <q-tab name="projects" label="New Projects" no-caps />
      </q-tabs>

      <q-tab-panels
        v-model="marketplaceTab"
        animated
        class="bg-transparent"
        transition-prev="jump-up"
        transition-next="jump-up"
      >
        <q-tab-panel name="services" class="q-pa-none">
          <div class="row q-col-gutter-md">
            <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="n in 4" :key="`service-${n}`">
              <q-intersection
                once
                transition="flip-right"
                :transition-duration="300"
                :style="`transition-delay: ${n * 100}ms`"
              >
                <q-card class="listing-card full-height" flat bordered>
                  <q-img
                    src="https://via.placeholder.com/300x180/ddeeff/77aaff?text=Service+Image+1"
                    height="180px"
                    :ratio="16 / 9"
                    class="card-img-zoom"
                  >
                    <q-chip
                      v-if="n === 1"
                      dense
                      color="orange"
                      text-color="white"
                      icon="star"
                      class="absolute-top-left q-ma-sm"
                      >Popular</q-chip
                    >
                    <q-chip
                      dense
                      color="blue-1"
                      text-color="primary"
                      class="absolute-top-right q-ma-sm"
                      >Marketing</q-chip
                    >
                  </q-img>
                  <q-card-section>
                    <div
                      class="text-subtitle1 text-weight-medium ellipsis-2-lines q-mb-xs"
                      style="min-height: 48px; line-height: 1.5"
                    >
                      Professional SEO Audit & Strategy Report {{ n }}
                    </div>
                    <div class="row items-center text-caption text-grey-7 q-mb-sm">
                      <q-rating
                        :model-value="4.9"
                        size="1.2em"
                        color="amber"
                        icon="star"
                        :max="5"
                        readonly
                        class="q-mr-xs"
                      />
                      <span class="text-weight-medium q-mr-xs">4.9</span>
                      <span>(120)</span>
                    </div>
                  </q-card-section>
                  <q-separator spaced />
                  <q-card-section class="row justify-between items-center q-pt-sm">
                    <div class="text-body1 text-weight-bold">From $250</div>
                    <q-btn
                      outline
                      dense
                      color="primary"
                      label="View"
                      size="sm"
                      no-caps
                      padding="xs md"
                      class="btn-hover-slide"
                    />
                  </q-card-section>
                </q-card>
              </q-intersection>
            </div>
          </div>
        </q-tab-panel>
        <q-tab-panel name="freelancers" class="q-pa-none">
          <div class="row q-col-gutter-md">
            <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="n in 4" :key="`freelancer-${n}`">
              <q-intersection
                once
                transition="flip-left"
                :transition-duration="300"
                :style="`transition-delay: ${n * 100}ms`"
              >
                <q-card class="listing-card full-height" flat bordered>
                  <q-card-section class="text-center">
                    <q-avatar size="100px" class="q-mb-md">
                      <img
                        :src="`https://via.placeholder.com/100x100/e0f2fe/0ea5e9?text=User+${n}`"
                      />
                    </q-avatar>
                    <div class="text-subtitle1 text-weight-medium q-mb-xs">
                      Alex Johnson {{ n }}
                    </div>
                    <div class="text-caption text-primary q-mb-sm">UI/UX Designer</div>
                    <q-rating
                      :model-value="4.8"
                      size="1em"
                      color="amber"
                      readonly
                      class="q-mb-sm"
                    />
                    <div class="row justify-center q-gutter-sm q-mb-md">
                      <q-chip dense color="blue-1" text-color="primary">Figma</q-chip>
                      <q-chip dense color="blue-1" text-color="primary">Web Design</q-chip>
                    </div>
                  </q-card-section>
                  <q-separator />
                  <q-card-section class="row justify-between items-center">
                    <div class="text-body1 text-weight-bold">$45/hr</div>
                    <q-btn
                      outline
                      dense
                      color="primary"
                      label="Profile"
                      size="sm"
                      no-caps
                      padding="xs md"
                      class="btn-hover-slide"
                    />
                  </q-card-section>
                </q-card>
              </q-intersection>
            </div>
          </div>
        </q-tab-panel>
        <q-tab-panel name="projects" class="q-pa-none">
          <div class="row q-col-gutter-md">
            <div class="col-12 col-sm-6" v-for="n in 4" :key="`project-${n}`">
              <q-intersection
                once
                transition="fade"
                :transition-duration="300"
                :style="`transition-delay: ${n * 100}ms`"
              >
                <q-card class="listing-card full-height" flat bordered>
                  <q-card-section>
                    <div class="text-h6 text-weight-medium q-mb-xs">
                      E-commerce Website Redesign {{ n }}
                    </div>
                    <div class="text-caption text-grey-7 q-mb-md">
                      Posted 2 days ago • Budget: $1,500-3,000
                    </div>
                    <p class="text-body2 ellipsis-3-lines">
                      Looking for an experienced web designer to revamp our online store. The
                      project includes updating the UI, improving mobile responsiveness, and
                      optimizing checkout flow.
                    </p>
                  </q-card-section>
                  <q-separator />
                  <q-card-section class="row justify-between items-center">
                    <div class="row q-gutter-x-sm">
                      <q-chip dense color="blue-1" text-color="primary">WordPress</q-chip>
                      <q-chip dense color="blue-1" text-color="primary">UI/UX</q-chip>
                    </div>
                    <q-btn
                      outline
                      dense
                      color="primary"
                      label="Details"
                      size="sm"
                      no-caps
                      padding="xs md"
                      class="btn-hover-slide"
                    />
                  </q-card-section>
                </q-card>
              </q-intersection>
            </div>
          </div>
        </q-tab-panel>
      </q-tab-panels>
      <div class="text-center q-mt-xl">
        <q-btn
          color="primary"
          label="Explore Full Marketplace"
          no-caps
          unelevated
          to="/marketplace"
          size="md"
          class="btn-glow"
        />
      </div>
    </section>

    <section id="experts" class="q-mb-xl q-mt-xl">
      <q-intersection once transition="slide-left">
        <h2 class="text-h4 text-weight-medium text-center text-slate-800 q-mb-xl section-title">
          Connect with Industry Experts
        </h2>
      </q-intersection>
      <div class="row q-col-gutter-lg justify-center">
        <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="n in 4" :key="`expert-${n}`">
          <q-intersection once transition="scale" :transition-delay="n * 100">
            <q-card class="expert-card text-center q-pa-md full-height" flat bordered>
              <q-card-section>
                <q-avatar size="100px" class="q-mb-md shadow-2 rotate-hover">
                  <img
                    :src="`https://via.placeholder.com/100/aabbcc/ffffff?text=E${n}`"
                    alt="Expert Avatar"
                  />
                  <q-badge v-if="n === 1" color="positive" floating rounded
                    ><q-icon name="verified" size="xs"
                  /></q-badge>
                </q-avatar>
                <div class="text-h6 q-mb-xs text-slate-800">Dr. Evelyn Reed {{ n }}</div>
                <div class="text-body2 text-grey-7 q-mb-md">Business Strategy Consultant</div>
                <div class="row justify-center items-center text-caption text-grey-8 q-gutter-x-md">
                  <span class="row items-center no-wrap"
                    ><q-icon name="star" color="amber" size="16px" class="q-mr-xs" /> 4.9</span
                  >
                  <span class="row items-center no-wrap"
                    ><q-icon name="military_tech" color="grey-6" size="16px" class="q-mr-xs" /> 15+
                    Yrs</span
                  >
                </div>
              </q-card-section>
              <q-card-actions align="center" class="q-pt-none">
                <q-btn
                  outline
                  dense
                  color="primary"
                  label="View Profile"
                  no-caps
                  padding="xs md"
                  class="btn-hover-slide"
                />
                <q-btn
                  color="primary"
                  label="Book"
                  no-caps
                  dense
                  unelevated
                  padding="xs md"
                  class="pulse-btn"
                />
              </q-card-actions>
            </q-card>
          </q-intersection>
        </div>
      </div>
      <div class="text-center q-mt-xl">
        <q-btn
          color="primary"
          label="Find More Experts"
          no-caps
          unelevated
          to="/consultants"
          size="md"
          class="btn-glow"
        />
      </div>
    </section>

    <section id="community" class="q-mb-xl q-mt-xl">
      <q-intersection once transition="slide-right">
        <h2 class="text-h4 text-weight-medium text-center text-slate-800 q-mb-xl section-title">
          Join the Conversation
        </h2>
      </q-intersection>
      <q-card flat bordered class="forum-card">
        <q-list separator>
          <div v-for="n in 3" :key="`topic-${n}`">
            <q-slide-item @left="onLeft" @right="onRight" left-color="info" right-color="warning">
              <template v-slot:left> <q-icon name="reply" /> Reply </template>
              <template v-slot:right> <q-icon name="flag" /> Flag </template>

              <q-item clickable v-ripple class="q-py-md forum-item">
                <q-item-section avatar top>
                  <q-avatar rounded color="blue-1" text-color="primary" icon="chat" />
                </q-item-section>
                <q-item-section>
                  <q-item-label
                    lines="1"
                    class="text-weight-medium text-body1 hover-underline cursor-pointer"
                    >Best practices for managing remote freelance teams? {{ n }}</q-item-label
                  >
                  <q-item-label caption lines="1">
                    Posted by <span class="text-weight-bold text-grey-8">Sarah Lee</span> in
                    <span class="text-primary cursor-pointer hover-underline"
                      >Freelancing Tips</span
                    >
                  </q-item-label>
                </q-item-section>
                <q-item-section side top class="text-caption text-grey-7 gt-sm">
                  <div class="row items-center q-gutter-sm q-mb-xs">
                    <span class="row items-center no-wrap"
                      ><q-icon name="forum" size="16px" class="q-mr-xs" /> 15</span
                    >
                    <span class="row items-center no-wrap"
                      ><q-icon name="visibility" size="16px" class="q-mr-xs" /> 1.2k</span
                    >
                  </div>
                  <div class="text-right">2 hours ago</div>
                </q-item-section>
              </q-item>
            </q-slide-item>
          </div>
        </q-list>
      </q-card>
      <div class="text-center q-mt-xl">
        <q-btn
          color="primary"
          label="Visit Community Forum"
          no-caps
          unelevated
          to="/community"
          size="md"
          class="btn-glow"
        />
      </div>
    </section>

    <section class="q-mb-xl q-mt-xl">
      <q-intersection once transition="scale">
        <h2 class="text-h4 text-weight-medium text-center text-slate-800 q-mb-xl section-title">
          Trusted by Professionals Like You
        </h2>
      </q-intersection>
      <q-carousel
        v-model="testimonialSlide"
        transition-prev="slide-right"
        transition-next="slide-left"
        swipeable
        animated
        control-color="primary"
        navigation
        padding
        arrows
        height="auto"
        class="bg-transparent testimonial-carousel"
        autoplay
        infinite
      >
        <q-carousel-slide :name="1" class="column no-wrap flex-center">
          <q-card flat bordered class="testimonial-card-inner q-pa-lg">
            <q-icon name="format_quote" size="40px" color="primary" style="opacity: 0.6" />
            <p class="text-italic text-body1 text-slate-700 q-mb-md" style="line-height: 1.8">
              "Game-changer for finding high-quality freelancers quickly. Smooth process, excellent
              talent!"
            </p>
            <div class="row items-center q-pt-sm">
              <q-avatar size="44px" class="q-mr-sm">
                <img src="https://via.placeholder.com/50/aabbff/ffffff?text=U1" />
              </q-avatar>
              <div>
                <div class="text-weight-medium text-slate-800">Michael B.</div>
                <div class="text-caption text-grey-7">CEO, Tech Startup</div>
              </div>
            </div>
          </q-card>
        </q-carousel-slide>
        <q-carousel-slide :name="2" class="column no-wrap flex-center">
          <q-card flat bordered class="testimonial-card-inner q-pa-lg">
            <q-icon name="format_quote" size="40px" color="primary" style="opacity: 0.6" />
            <p class="text-italic text-body1 text-slate-700 q-mb-md" style="line-height: 1.8">
              "Found the perfect consultant for my business strategy within hours. The booking
              system is seamless."
            </p>
            <div class="row items-center q-pt-sm">
              <q-avatar size="44px" class="q-mr-sm">
                <img src="https://via.placeholder.com/50/ffccaa/ffffff?text=U2" />
              </q-avatar>
              <div>
                <div class="text-weight-medium text-slate-800">Anusha P.</div>
                <div class="text-caption text-grey-7">Small Business Owner</div>
              </div>
            </div>
          </q-card>
        </q-carousel-slide>
        <q-carousel-slide :name="3" class="column no-wrap flex-center">
          <q-card flat bordered class="testimonial-card-inner q-pa-lg">
            <q-icon name="format_quote" size="40px" color="primary" style="opacity: 0.6" />
            <p class="text-italic text-body1 text-slate-700 q-mb-md" style="line-height: 1.8">
              "The community forum is incredibly helpful. I've learned so much from other
              professionals in my field."
            </p>
            <div class="row items-center q-pt-sm">
              <q-avatar size="44px" class="q-mr-sm">
                <img src="https://via.placeholder.com/50/ccddff/ffffff?text=U3" />
              </q-avatar>
              <div>
                <div class="text-weight-medium text-slate-800">Raj S.</div>
                <div class="text-caption text-grey-7">Freelance Developer</div>
              </div>
            </div>
          </q-card>
        </q-carousel-slide>
      </q-carousel>
    </section>

    <section class="cta-section q-mt-xl q-mb-lg">
      <q-intersection once transition="jump-up">
        <div
          class="bg-gradient-primary text-white q-pa-xl rounded-borders text-center shadow-4 cta-container"
        >
          <div class="cta-particles"></div>
          <h2 class="text-h4 text-weight-bold q-mb-md">ඔබේ සාර්ථකත්වය අදම අරඹන්න!</h2>
          <p class="text-body1 q-mb-lg" style="opacity: 0.9; max-width: 600px; margin: auto">
            අපගේ වේදිකාවට අදම ලියාපදිංචි වන්න. අවස්ථා සොයාගන්න, දක්ෂයින් බඳවාගන්න, හෝ විශේෂඥ උපදෙස්
            ලබාගන්න.
          </p>
          <div class="q-gutter-md">
            <q-btn
              size="lg"
              color="white"
              text-color="primary"
              label="නොමිලේ ලියාපදිංචි වන්න!"
              no-caps
              unelevated
              padding="sm xl"
              icon="person_add"
              class="cta-primary-btn"
            />
            <q-btn
              size="lg"
              flat
              text-color="white"
              label="වැඩි විස්තර"
              no-caps
              style="border: 1px solid rgba(255, 255, 255, 0.5)"
              icon-right="info"
              class="cta-secondary-btn"
            />
          </div>
        </div>
      </q-intersection>
    </section>
  </q-page>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue' // Import onUnmounted
import { useQuasar } from 'quasar'

const $q = useQuasar()
const searchQuery = ref('')
const marketplaceTab = ref('services')
const testimonialSlide = ref(1)
const searchFocused = ref(false)

// Declare intervalId outside hooks
let intervalId = null

const features = ref([
  {
    icon: 'work_outline',
    title: 'Freelance වෙළඳපොළ',
    description:
      'ඕනෑම project එකකට ගැලපෙන දක්ෂ, තහවුරු කළ freelancers ලා දහස් ගණනක් අතරින් තෝරාගන්න.',
    btnLabel: 'Marketplace එක බලන්න',
    link: '/marketplace',
    color: 'blue',
  },
  {
    icon: 'local_mall',
    title: 'වෘත්තීය සේවා',
    description:
      'ස්ථාවර මිල ගණන් යටතේ, අලෙවිකරණය, නිර්මාණකරණය, ලිවීම වැනි විවිධ සේවා පැකේජ පහසුවෙන් ලබාගන්න.',
    btnLabel: 'සේවා නාමාවලිය',
    link: '/services',
    color: 'green',
  },
  {
    icon: 'groups',
    title: 'විශේෂඥ උපදේශන',
    description:
      'ඔබේ ව්‍යාපාරයේ හෝ වෘත්තියේ අභියෝග ජයගැනීමට පළපුරුදු, ඉහළ පෙළේ උපදේශකයින්ගෙන් මගපෙන්වීම් ලබාගන්න.',
    btnLabel: 'උපදේශකයින් සොයන්න',
    link: '/consultants',
    color: 'purple',
  },
  {
    icon: 'forum',
    title: 'ක්‍රියාකාරී ප්‍රජාව',
    description:
      'අදහස් බෙදාගන්න, ප්‍රශ්න අසන්න, අත්දැකීම් හුවමාරු කරගන්න, සහ අනෙකුත් වෘත්තිකයන් සමඟ ජාලගත වන්න.',
    btnLabel: 'ප්‍රජාවට එක්වන්න',
    link: '/community',
    color: 'red',
  },
])

function performSearch() {
  if (!searchQuery.value) {
    $q.notify({
      color: 'warning', // Changed color
      position: 'top',
      message: 'Please enter a search term.',
      icon: 'warning',
    })
    return
  }
  console.log('Searching for:', searchQuery.value)
  $q.notify({
    color: 'info', // Changed color
    position: 'top',
    message: `Searching for "${searchQuery.value}"...`,
    icon: 'search',
  })
  // Implement actual search logic or navigation here
}

function onLeft({ reset }) {
  $q.notify('Left action triggered. Add reply logic.')
  reset()
}
function onRight({ reset }) {
  $q.notify('Right action triggered. Add flag logic.')
  reset()
}

onMounted(() => {
  // Auto-slide testimonials
  intervalId = setInterval(() => {
    // Assign to outer variable
    testimonialSlide.value = (testimonialSlide.value % 3) + 1 // Assuming 3 slides
  }, 7000)
})

onUnmounted(() => {
  // Clear the interval when the component is unmounted
  if (intervalId) {
    clearInterval(intervalId)
    console.log('Testimonial interval cleared.') // Optional: for debugging
  }
})
</script>

<style scoped>
/* --- Base & Gradients --- */
.bg-gradient-primary {
  background: linear-gradient(135deg, var(--q-primary), #1d4ed8); /* blue-700 */
}
.bg-slate-50 {
  background-color: #f8fafc;
}
.text-slate-600 {
  color: #475569;
}
.text-slate-800 {
  color: #1e293b;
}

/* --- Section Title --- */
.section-title {
  position: relative;
  display: inline-block;
  padding-bottom: 10px;
  margin-left: auto;
  margin-right: auto;
}
.section-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 3px;
  background: linear-gradient(90deg, transparent, var(--q-primary), transparent);
  border-radius: 2px;
}

/* --- Hero Section --- */
.hero-section {
  position: relative;
  z-index: 1;
}
.floating-shapes {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  pointer-events: none;
}
.floating-shape {
  position: absolute;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 40%;
  animation: float 25s infinite ease-in-out alternate;
}
.shape-1 {
  width: 80px;
  height: 80px;
  top: 10%;
  left: 15%;
  animation-delay: 0s;
}
.shape-2 {
  width: 60px;
  height: 60px;
  top: 65%;
  left: 75%;
  animation-delay: 2s;
  border-radius: 50% 30% 60% 40%;
}
.shape-3 {
  width: 40px;
  height: 40px;
  top: 43%;
  left: 5%;
  animation-delay: 4s;
}
.shape-4 {
  width: 100px;
  height: 100px;
  top: 76%;
  left: 45%;
  animation-delay: 6s;
  border-radius: 30% 50% 40% 60%;
}
.shape-5 {
  width: 50px;
  height: 50px;
  top: 19%;
  left: 85%;
  animation-delay: 8s;
}
.shape-6 {
  width: 70px;
  height: 70px;
  top: 40%;
  left: 95%;
  animation-delay: 10s;
  border-radius: 60% 40% 30% 50%;
}
@keyframes float {
  0% {
    transform: translateY(0px) rotate(0deg) scale(1);
  }
  100% {
    transform: translateY(-30px) rotate(15deg) scale(1.05);
  }
}

/* Fade-in Animations */
.animate-fade-in {
  animation: fadeIn 1s ease 0.1s forwards;
  opacity: 0;
}
.animate-fade-in-delay-1 {
  animation: fadeIn 1s ease 0.4s forwards;
  opacity: 0;
}
.animate-fade-in-delay-2 {
  animation: fadeIn 1s ease 0.7s forwards;
  opacity: 0;
}
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Search Input Focus Effect */
.custom-search-input {
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
}
.custom-search-input .q-field__control {
  border-radius: 30px !important;
}
.custom-search-input .q-field__append {
  padding-right: 6px;
}
.search-focused .q-field__control {
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.2);
}
.search-btn {
  transition: all 0.3s ease;
}
.search-btn:hover {
  transform: scale(1.05);
}

/* --- Feature Cards --- */
.feature-card {
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
  position: relative;
  padding-bottom: 70px;
  border-color: #e2e8f0;
  border-radius: 12px;
  overflow: hidden;
}
.feature-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: linear-gradient(90deg, var(--q-primary), var(--q-secondary));
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.4s ease-out;
}
.feature-card:hover {
  transform: translateY(-6px);
  box-shadow: var(--q-shadow-5);
}
.feature-card:hover::before {
  transform: scaleX(1);
}
.feature-card .q-card-actions {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: white;
  padding-top: 8px;
}
.pulse-avatar {
  animation: pulse-light 2.5s infinite cubic-bezier(0.4, 0, 0.6, 1);
}
@keyframes pulse-light {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
}

/* --- Cards (Listing, Expert) --- */
.listing-card,
.expert-card {
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease,
    border-color 0.3s ease;
  border-color: #e2e8f0;
  border-radius: 12px;
  overflow: hidden;
}
.listing-card:hover,
.expert-card:hover {
  transform: translateY(-6px);
  box-shadow: var(--q-shadow-4);
  border-color: var(--q-primary);
}
.card-img-zoom > .q-img__content,
.card-img-zoom > img {
  transition: transform 0.5s ease;
}
.card-img-zoom:hover > .q-img__content,
.card-img-zoom:hover > img {
  transform: scale(1.05);
}
.rotate-hover:hover .q-avatar img {
  transform: rotate(10deg);
  transition: transform 0.5s ease;
}

/* --- Button Hover Effects --- */
.btn-hover-effect {
  transition: background-color 0.3s ease;
}
.btn-hover-slide {
  position: relative;
  overflow: hidden;
  transition:
    color 0.3s ease,
    border-color 0.3s ease;
  z-index: 1;
}
.btn-hover-slide::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 0;
  height: 100%;
  background-color: var(--q-primary);
  transition: width 0.3s ease;
  z-index: -1;
  border-radius: inherit;
}
.btn-hover-slide:hover {
  color: white !important;
  border-color: var(--q-primary) !important;
}
.btn-hover-slide:hover::before {
  width: 100%;
}
.btn-glow {
  box-shadow: 0 0 8px rgba(37, 99, 235, 0.3);
  transition: all 0.3s ease;
}
.btn-glow:hover {
  box-shadow: 0 0 16px rgba(37, 99, 235, 0.5);
  transform: translateY(-2px);
}
.pulse-btn {
  animation: pulse-btn 2s infinite cubic-bezier(0.4, 0, 0.6, 1);
}
@keyframes pulse-btn {
  0%,
  100% {
    transform: scale(1);
    box-shadow: 0 0 0 0 rgba(37, 99, 235, 0.4);
  }
  50% {
    transform: scale(1.02);
    box-shadow: 0 0 0 8px rgba(37, 99, 235, 0);
  }
}

/* --- Forum --- */
.forum-card {
  border-radius: 12px;
  overflow: hidden;
  transition: box-shadow 0.3s ease;
}
.forum-item {
  transition: background-color 0.3s ease;
}
.forum-item:hover {
  background-color: #f0f7ff;
}

/* --- Testimonials --- */
.testimonial-carousel {
  border-radius: 12px;
}
.testimonial-card-inner {
  border-left: 4px solid var(--q-primary);
  background-color: white;
  width: 95%;
  max-width: 600px;
  margin: auto;
  border-radius: 8px;
  box-shadow: var(--q-shadow-2);
}

/* --- CTA --- */
.cta-container {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
}
.cta-particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  background-image: radial-gradient(circle, rgba(255, 255, 255, 0.06) 1px, transparent 1px);
  background-size: 25px 25px;
  animation: moveParticles 80s linear infinite;
}
@keyframes moveParticles {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 600px 600px;
  }
}
.cta-primary-btn {
  transition: all 0.3s ease;
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
}
.cta-primary-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 12px 20px rgba(0, 0, 0, 0.15);
}
.cta-secondary-btn {
  transition: all 0.3s ease;
}
.cta-secondary-btn:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: white;
}

/* --- Entry Animations --- */
.feature-anim-enter-active {
  transition: all 0.6s cubic-bezier(0.25, 0.8, 0.25, 1);
  transition-delay: calc(0.08s * var(--feature-index));
}
.feature-anim-leave-active {
  transition: all 0.4s cubic-bezier(0.55, 0.055, 0.675, 0.19);
}
.feature-anim-enter-from,
.feature-anim-leave-to {
  opacity: 0;
  transform: translateY(40px) scale(0.95);
}

/* --- Utils --- */
.full-height {
  height: 100%;
}
.ellipsis-2-lines {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.ellipsis-3-lines {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.hover-underline:hover {
  text-decoration: underline;
}

/* --- Responsive --- */
@media (max-width: 600px) {
  .text-h2 {
    font-size: 1.75rem;
  }
  .text-h3 {
    font-size: 1.5rem;
  }
  .text-h4 {
    font-size: 1.3rem;
  }
  .hero-section {
    padding-top: 2rem;
    padding-bottom: 3rem;
  }
  .q-tabs {
    flex-wrap: wrap;
    height: auto;
  }
  .floating-shapes {
    display: none;
  }
  .testimonial-card-inner {
    width: 95%;
  }
}
</style>

oyata puluwanda meke code eka tawa simple karanna mata pahadilima nati tan godak tiyanawa
