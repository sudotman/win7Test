<template>
  <div
    :class="$style.taskbarRepo"
    @click.capture="showPopup"
  >
    <img :src="logoSrc">
    <Popup
      v-model:visible="popup"
      :class="$style.popupStyle"
    >
      <div :class="$style.popup">
        <div>
          You can checkout my github! <a
            href="https://github.com/sudotman"
            target="__blank"
          >Github Link</a>!
        </div>
        <br>
       
      </div>
    </Popup>
  </div>
</template>

<script>
import { rgba } from '@/styles/utils';
import { panelSize } from '@/styles/constants';
import Popup from '@/components/Popup.vue';
import { resolveFileByPath } from '@/services/fs';

export default {
  components: {
    Popup,
  },
  data() {
    return {
      popup: false,
    };
  },
  computed: {
    logoSrc() {
      return resolveFileByPath('C:/Windows/system/icons/github.png').data;
    },
  },
  methods: {
    showPopup() {
      this.popup = true;
    },
  },
  style({ className }) {
    return [
      className('taskbarRepo', {
        display: 'flex',
        flexDirection: 'row',
        alignItems: 'center',
        '& > img': {
          width: '22px',
          height: '22px',
          padding: '2px',
          borderRadius: '5px',
          overflow: 'hidden',
          cursor: 'pointer',
          background: '#fff',
        },
      }),
      className('popupStyle', {
        right: '15px',
        bottom: `${parseInt(panelSize, 10) + 15}px`,
      }),
      className('popup', {
        background: rgba(255, 1),
        borderRadius: '6px',
        padding: '15px',
        width: '280px',
        textAlign: 'justify',
        border: `solid 1px ${rgba(0, 0.5)}`,
        '& a': {
          textDecoration: 'underline',
        },
      }),
    ];
  },
};
</script>
