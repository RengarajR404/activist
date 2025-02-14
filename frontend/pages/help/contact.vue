<template>
  <div
    class="text-light-text dark:text-dark-text bg-light-content dark:bg-dark-content"
  >
    <Head>
      <Title>{{ $t("pages.help.contact.title") }}</Title>
    </Head>
    <PageDocs
      imgURL="/images/content_pages/icons/bootstrap_envelope"
      imgAltText="pages.help.contact.img-alt-text"
    >
      <div
        v-if="!emailSent"
        class="items-center text-left space-y-4 md:items-start"
      >
        <h1 class="pb-2 font-bold responsive-h1">
          {{ $t("pages.help.contact.header") }}
        </h1>
        <div class="flex flex-row py-2 space-x-3">
          <Icon
            class="text-light-link-text dark:text-dark-link-text mt-[0.125rem]"
            name="bi:info-circle-fill"
            size="1.25em"
          />
          <p>
            {{ $t("pages.help.faq.subheader-1") }}
            <a
              class="items-center focus-brand link-text"
              href="https://matrix.to/#/#activist_community:matrix.org"
              target="_blank"
            >
              {{ $t("pages.help.faq.subheader-2") }}
              <Icon
                name="bi:box-arrow-up-right"
                size="1em"
                style="vertical-align: baseline"
              />
            </a>
            !
          </p>
        </div>
        <div class="flex flex-col space-y-4 lg:space-y-6">
          <p>
            {{ $t("pages.help.contact.section-1-paragraph-1-1") }}
            <a
              class="items-center focus-brand link-text"
              href="https://matrix.to/#/#activist_community:matrix.org"
            >
              {{ $t("pages.help.contact.section-1-paragraph-1-2") }}
              <Icon
                name="bi:box-arrow-up-right"
                size="1em"
                style="vertical-align: baseline"
              />
            </a>
            {{ $t("pages.help.contact.section-1-paragraph-1-3") }}
            <a
              class="items-center focus-brand link-text"
              href="https://github.com/activist-org/activist"
            >
              {{ $t("pages.help.contact.section-1-paragraph-1-4") }}
              <Icon
                name="bi:box-arrow-up-right"
                size="1em"
                style="vertical-align: baseline"
              />
            </a>
            {{ $t("pages.help.contact.section-1-paragraph-1-5") }}
          </p>
          <p>
            {{ $t("pages.help.contact.section-1-paragraph-2-1") }}
            <a
              class="items-center focus-brand link-text"
              href="https://github.com/activist-org/activist/blob/main/.github/CODE_OF_CONDUCT.md"
              target="_blank"
            >
              {{ $t("pages.help.contact.section-1-paragraph-2-2") }}
              <Icon
                name="bi:box-arrow-up-right"
                size="1em"
                style="vertical-align: baseline"
              /> </a
            >.
          </p>
        </div>
        <div>
          <form @submit.prevent="sendEmail" class="flex flex-col space-y-4">
            <div class="flex flex-col space-y-2">
              <label
                :class="{
                  'text-red-500': !nameValidated,
                  'text-light-text dark:text-dark-text': nameValidated,
                }"
                for="name"
                >{{ $t("pages.help.contact.label-name") }}
                <span v-if="!nameValidated">{{
                  $t("pages.help.contact.error-empty")
                }}</span></label
              >
              <input
                v-model="name"
                @blur="validateName"
                class="p-2 rounded-md placeholder:dark:dark-placeholder placeholder:light-placeholder placeholder:italic bg-light-highlight dark:bg-dark-highlight focus:bg-light-distinct focus:dark:bg-dark-distinct text-light-text dark:text-dark-text"
                :class="{
                  'outline-red-500 outline outline-2': !nameValidated,
                  'outline-none focus:outline-none': nameValidated,
                }"
                :placeholder="$t('pages.help.contact.placeholder-name')"
                autocomplete="off"
                spellcheck="false"
                id="name"
              />
            </div>
            <div class="flex flex-col space-y-2">
              <label
                :class="{
                  'text-red-500': !emailValidated,
                  'text-light-text dark:text-dark-text': emailValidated,
                }"
                for="email"
                >{{ $t("pages.help.contact.label-email") }}
                <span v-if="!emailValidated"
                  >{{
                    $t("pages.help.contact.valid")
                  }}
                  (example@mail.com).</span
                ></label
              >
              <input
                v-model="email"
                @blur="validateEmail"
                class="p-2 rounded-md placeholder:dark:dark-placeholder placeholder:light-placeholder placeholder:italic bg-light-highlight dark:bg-dark-highlight focus:bg-light-distinct focus:dark:bg-dark-distinct text-light-text dark:text-dark-text"
                :class="{
                  'outline-red-500 outline outline-2': !emailValidated,
                  'outline-none focus:outline-none': emailValidated,
                }"
                placeholder="example@mail.com"
                autocomplete="off"
                spellcheck="false"
                id="email"
              />
            </div>
            <div class="flex flex-col space-y-2">
              <label
                :class="{
                  'text-red-500': !messageValidated,
                  'text-light-text dark:text-dark-text': messageValidated,
                }"
                for="message"
                >{{ $t("pages.help.contact.label-message") }}
                <span v-if="!messageValidated">cannot be empty.</span></label
              >
              <textarea
                v-model="message"
                @blur="validateMessage"
                :class="{
                  'outline-red-500 outline outline-2': !messageValidated,
                  'outline-none focus:outline-none': messageValidated,
                }"
                rows="6"
                :placeholder="$t('pages.help.contact.placeholder-message')"
                class="p-2 resize-none rounded-md placeholder:dark:dark-placeholder placeholder:light-placeholder placeholder:italic bg-light-highlight dark:bg-dark-highlight focus:bg-light-distinct focus:dark:bg-dark-distinct text-light-text dark:text-dark-text"
                autocomplete="off"
                spellcheck="false"
                id="message"
              ></textarea>
            </div>
            <button
              class="flex items-center px-4 py-2 font-semibold text-center border select-none rounded-md xl:rounded-lg focus-brand w-fit shadow-sm shadow-zinc-700 text-light-text border-light-text dark:text-dark-cta-orange dark:border-dark-cta-orange fill-light-text dark:fill-dark-cta-orange bg-light-cta-orange dark:bg-dark-cta-orange/10"
              :class="{
                'cursor-not-allowed': buttonDisabled,
                'hover:bg-light-cta-orange-hover active:bg-light-cta-orange dark:hover:bg-dark-cta-orange-hover/25 dark:active:bg-dark-cta-orange/10':
                  !buttonDisabled,
              }"
              type="submit"
              :disabled="buttonDisabled"
              :aria-label="$t('pages.contact.send-form-aria-label')"
            >
              {{ $t("pages.help.contact.send") }}
            </button>
          </form>
        </div>
      </div>
      <div
        v-else
        class="flex flex-col items-center justify-center md:items-start md:text-start pb-8 text-center space-y-4 md:space-y-6"
      >
        <h1 class="pb-2 font-bold responsive-h1">
          {{ $t("pages.help.contact.thanks-1") }}
        </h1>
        <div class="flex flex-row text-start py-2 space-x-3">
          <Icon
            class="text-light-link-text dark:text-dark-link-text mt-[0.125rem]"
            name="bi:info-circle-fill"
            size="1.25em"
          />
          <p>
            {{ $t("pages.help.faq.subheader-1") }}
            <a
              class="items-center focus-brand link-text"
              href="https://matrix.to/#/#activist_community:matrix.org"
              target="_blank"
            >
              {{ $t("pages.help.faq.subheader-2") }}
              <Icon
                name="bi:box-arrow-up-right"
                size="1em"
                style="vertical-align: baseline"
              />
            </a>
            !
          </p>
        </div>
        <p>
          {{ $t("pages.help.contact.thanks-2") }}
        </p>
        <BtnLabeled
          :cta="false"
          label="components.btn-labeled.return-home"
          linkTo="/"
          fontSize="lg"
          ariaLabel="components.btn-labeled.return-home-aria-label"
        />
      </div>
    </PageDocs>
  </div>
</template>

<script setup lang="ts">
const name = ref("");
const email = ref("");
const message = ref("");
const nameValidated = ref(true);
const emailValidated = ref(true);
const messageValidated = ref(true);
const buttonDisabled = ref(true);
const mail = useMail();
const emailSent = ref(false);

const validateEmail = () => {
  if (!email.value.match(/.*@\w+\.\w+/)) {
    emailValidated.value = false;
  }
};

const validateMessage = () => {
  if (message.value.trim().length === 0) {
    messageValidated.value = false;
  }
};

const validateName = () => {
  if (name.value.trim().length === 0) {
    nameValidated.value = false;
  }
};
watch(name, () => {
  if (name.value.length > 0) {
    nameValidated.value = true;
  }
});

watch(email, () => {
  if (email.value.match(/.*@\w+\.\w+/)) {
    emailValidated.value = true;
  }
});

watch(message, () => {
  if (message.value.length > 0) {
    messageValidated.value = true;
  }
});

watch([message, email, name], () => {
  if (
    name.value.trim().length > 0 &&
    email.value.match(/.*@\w+\.\w+/) &&
    message.value.trim().length > 0
  ) {
    buttonDisabled.value = false;
  } else {
    buttonDisabled.value = true;
  }
});

const sendEmail = async () => {
  if (
    name.value.trim().length > 0 &&
    email.value.match(/.*@\w+\.\w+/) &&
    message.value.trim().length > 0
  ) {
    await mail.send({
      from: email.value,
      subject: `activist contact form from ${name.value}`,
      text: message.value,
    });
    emailSent.value = true;
  }
};
</script>
