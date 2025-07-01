<template>
  <div class="fixed inset-0 flex items-center z-[100] max-[700px]:px-[20px]" @click.self="close">
    <div class="modalContent relative bg-white w-[580px] left-[clamp(1.25rem,-0.724rem+10.526vw,8.75rem)] pt-[clamp(1.5rem,0.711rem+4.211vw,4.5rem)] pb-[clamp(1.5rem,0.711rem+4.211vw,4.5rem)] pr-[clamp(1.5rem,0.809rem+3.684vw,4.125rem)] pl-[clamp(1.5rem,0.809rem+3.684vw,4.125rem)]" :class="{
  modalEnter: animateIn && !animateOut,
  modalExit: animateOut
}">
      <button class="modalClose absolute cursor-pointer z-[100]
         opacity-0" @click="close" :class="{ modalFadeIn: fadeInDetails }">
        <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 15 15" fill="none">
          <path
              d="M7.47211 6.08565L13.3347 0L14.8426 1.44954L8.93825 7.31805L15 13.1986L13.4303 14.8552L7.65339 8.91838L1.751 15L0.129482 13.4359C2.12151 11.4596 4.05777 9.55167 6.04781 7.58745L0 1.65259L1.55378 0L7.47211 6.08565Z"
              fill="#611818"/>
        </svg>
      </button>
      <div class="modalContentFlex flex flex-col gap-[clamp(0.75rem,0.487rem+1.404vw,1.75rem)]
         opacity-0 " :class="{ modalFadeIn: fadeInDetails }">
        <h2 class="text-[#611818] font-[Didot,serif] text-[clamp(2.875rem,2.546rem+1.754vw,4.125rem)] font-bold not-italic leading-none m-0">
          Explore</h2>
        <p class="text-[#282828] font-[Lato,sans-serif] text-[clamp(0.875rem,0.809rem+0.351vw,1.125rem)] not-italic font-normal leading-[22px] tracking-[0.35px] m-0">
          Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque
          laudantium, totam rem
          aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.
          Nemo
          enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos
          qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet,
          consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam
          aliquam
          quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam,
          nisi ut aliquid ex ea commodi consequatur?</p>
        <a
            href="https://www.udundi.com/"
            target="_blank"
            rel="noopener"
            class="no-underline"
        >
          <button class="modalReadMoreButton">
            <span>Read More</span>
          </button>
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref, onMounted, nextTick} from 'vue'

// Props & Emit Setup
defineProps(['show'])
const emit = defineEmits(['close'])

// Animation State
const animateIn = ref(false)
const animateOut = ref(false)
const fadeInDetails = ref(false)

// Close modal with exit animation
function close() {
  animateOut.value = true
  fadeInDetails.value = false

  // Wait for exit animation to finish before fully closing
  setTimeout(() => {
    emit('close')
    animateIn.value = false
    animateOut.value = false
  }, 400) // Match the transition duration in CSS
}

// Handle enter animation on mount
onMounted(() => {
  setTimeout(() => {
    animateIn.value = true
    nextTick(() => {
      setTimeout(() => {
        fadeInDetails.value = true
      }, 10) // Small delay to allow CSS transition stagger
    })
  }, 10)
})
</script>


<style scoped>

.modalContent {
  padding: clamp(1.5rem, 0.711rem + 4.211vw, 4.5rem) clamp(1.5rem, 0.809rem + 3.684vw, 4.125rem);
  clip-path: polygon(8% 7%, 50% 0, 92% 7%, 100% 40%, 95% 90%, 50% 100%, 5% 90%, 0 40%);
  transform: scale(0.2);
  transform-origin: bottom left;
  opacity: 0;
  transition: clip-path 0.4s ease-out,
  transform 0.3s ease-out,
  opacity 0.1s ease-out;
}

@media screen and (max-width: 700px) {
  .modalContent {
    width: 100%;
    left: 0;
  }
}

.modalEnter {
  clip-path: polygon(0 0, 50% 0, 100% 0, 100% 40%, 100% 100%, 50% 100%, 0 100%, 0 40%);
  transform: scale(1);
  opacity: 1;
}

.modalExit {
  clip-path: polygon(8% 7%, 50% 0, 92% 7%, 100% 40%, 95% 90%, 50% 100%, 5% 90%, 0 40%);
  transform: scale(0.2);
  opacity: 0;
  transition: clip-path 0.4s ease-in,
  transform 0.3s ease-in,
  opacity 0.3s ease-in;
}

.modalClose {
  top: clamp(0.375rem, 0.063rem + 1.667vw, 1.563rem);
  right: clamp(0.375rem, 0.063rem + 1.667vw, 1.563rem);
  transform: translateX(-20px);
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.modalContentFlex {
  transform: translateX(-20px);
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.modalFadeIn {
  opacity: 1 !important;
  transform: translateX(0) !important;
  transition: opacity 0.4s ease 0.3s, transform 0.4s ease 0.3s;
}

.modalReadMoreButtonLink {
  text-decoration: none;
}

.modalReadMoreButton {
  position: relative;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  padding: 16px 57px;
  flex-shrink: 0;
  background: linear-gradient(90deg, #611818 0%, #A36754 100%);
  border: none;
  color: #FFF;
  font-family: Lato, sans-serif;
  font-size: clamp(0.875rem, 0.809rem + 0.351vw, 1.125rem);
  font-weight: 700;
  letter-spacing: 1.693px;
  text-transform: uppercase;
  cursor: pointer;
  transition: transform 0.3s ease, border-radius 0.3s ease;
}

.modalReadMoreButton::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, #A36754 0%, #611818 100%);
  opacity: 0;
  transition: opacity 0.4s ease;
  z-index: 0;
}

.modalReadMoreButton:hover::before {
  opacity: 1;
}

.modalReadMoreButton:hover {
  transform: scale(1.05);
  border-radius: 12px;
}

.modalReadMoreButton span {
  position: relative;
  z-index: 1;
}

</style>
