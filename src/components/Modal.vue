<template>
  <div class="modalOverlay" @click.self="close">
    <div class="modalContent">
      <button class="modalClose" @click="close">
        <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 15 15" fill="none">
          <path
              d="M7.47211 6.08565L13.3347 0L14.8426 1.44954L8.93825 7.31805L15 13.1986L13.4303 14.8552L7.65339 8.91838L1.751 15L0.129482 13.4359C2.12151 11.4596 4.05777 9.55167 6.04781 7.58745L0 1.65259L1.55378 0L7.47211 6.08565Z"
              fill="#611818"/>
        </svg>
      </button>
      <div class="modalContentFlex">
        <h2 class="modalHeading">Explore</h2>
        <p class="modalText">Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque
          laudantium, totam rem
          aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.
          Nemo
          enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos
          qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet,
          consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam
          aliquam
          quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam,
          nisi ut aliquid ex ea commodi consequatur?</p>
        <button class="modalReadMoreButton">Read More</button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps(['show'])
const emit = defineEmits(['close'])

function close() {
  emit('close')
}
</script>

<style scoped>
.modalOverlay {
  position: fixed;
  inset: 0;
  display: flex;
  align-items: center;
  z-index: 100;
}

.modalContent {
  position: relative;
  left: 140px;
  background: white;
  width: 580px;
  padding: 72px 66px
}

.modalClose {
  position: absolute;
  top: 25px;
  right: 25px;
  background: transparent;
  font-size: 1.5rem;
  border: none;
  cursor: pointer;
}

.modalContentFlex {
  display: flex;
  flex-direction: column;
  gap: 28px
}

.modalHeading {
  color: #611818;
  font-family: Didot, serif;
  font-size: 66px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  margin: 0;
}

.modalText {
  color: #282828;
  font-family: Lato, sans-serif;
  font-size: 18px;
  font-style: normal;
  font-weight: 400;
  line-height: 22px;
  letter-spacing: 0.35px;
}

.modalReadMoreButton {
  display: flex;
  width: 235px;
  height: 55px;
  padding: 16px 57px;
  justify-content: center;
  align-items: center;
  gap: 10px;
  flex-shrink: 0;
  background: linear-gradient(90deg, #611818 0%, #A36754 100%);
  border: none;
  color: #FFF;

  text-align: center;
  font-family: Lato;
  font-size: 18px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  letter-spacing: 1.693px;
  text-transform: uppercase;
}
</style>
