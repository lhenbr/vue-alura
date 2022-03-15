 <template>
  <button class="button" @click="clicked">
    <span class="icon">
      <i :class="icone"></i>
    </span>
    <span>{{ texto }}</span>
  </button>
</template>
<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  // eslint-disable-next-line
  name: "Button",
  props: {
    texto: {
      type: String,
      default: "button",
    },
    icone: {
      type: String,
      required: true,
    },
  },
  emits: ["clicked"],
  methods: {
    clicked() {
      this.$emit("clicked");
    },
  },
});
</script>