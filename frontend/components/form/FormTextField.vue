<template>
  <div
    class="flex items-center pl-[12px] pr-[10px] py-2 max-h-[40px] space-x-2 text-left border rounded select-none border-light-interactive dark:border-dark-interactive text-light-special-text dark:text-dark-special-text"
  >
    <input
      class="w-full h-5 bg-transparent outline-none placeholder:text-light-special-text dark:placeholder:text-dark-special-text"
      @input="updateValue"
      :id="uuid"
      :value="modelValue"
      :placeholder="placeholder"
      :type="refInputType"
    />
    <span v-if="isIconVisible" @click="changeInputType" class="cursor-pointer">
      <Icon name="mdi:eye" size="28px" />
    </span>
  </div>
</template>

<script setup lang="ts">
import useFormInput from "../../composables/useFormSetup";
import useUniqueID from "../../composables/useUniqueID";

const props = defineProps({
  placeholder: {
    type: string,
    default: "",
  },
  modelValue: {
    type: string,
    default: "",
  },
  inputType: {
    type: string,
    default: "text",
  },
  isIconVisible: {
    type: boolean,
    default: false,
  },
});
const emit = defineEmits(["update:modelValue"]);

const { updateValue } = useFormInput({ value: props?.modelValue }, emit, false);

const uuid = useUniqueID().getID();

const refInputType = ref(props?.inputType);

const changeInputType = () => {
  refInputType.value = refInputType.value === "password" ? "text" : "password";
};
</script>
