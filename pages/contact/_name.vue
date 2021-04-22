<template>
  <div class="container mx-auto px-4">
    <div class="flex items-center p-0 sm:p-5">
      <div class="contact-avatar relative rounded-full w-20 h-20">
        <img class="absolute inset-0 m-auto w-1/2" src="/images/blip.png" />
      </div>
      <div class="ml-5">
        <span class="contact-name font-bold">{{ contact.name }}</span>
        <span class="block font-semibold">id: {{ contact.shortName }}</span>
      </div>
      <span class="contact-date ml-auto font-semibold text-center w-1/3 sm:w-max">
        Created at {{ contact.created | date }}
      </span>
    </div>
    <hr class="mt-5 mb-8 border-2 border-gray-300 bg-gray-300" />
    <div class="flex flex-wrap">
      <div class="w-full xl:w-2/3">
        <div class="grid grid-cols-1 sm:grid-cols-4 md:grid-cols-12 gap-4">
          <div
            class="info-card sm:col-span-2 md:col-span-5 lg:col-span-4 bg-white rounded-xl shadow-lg p-10 h-64 text-center sm:text-left"
          >
            <span class="title block font-semibold mb-2 text-sm"
              >Region and idiom</span
            >
            <span class="block font-semibold text-sm"
              >Brazil - Portuguese (PT)</span
            >
            <span class="title block font-semibold mt-5 mb-2 text-sm"
              >Timezone</span
            >
            <span class="block font-semibold text-sm"
              >(UTC - 03:00) Brasilia</span
            >
          </div>
          <analytics-card
            bg-color="#2cc3d5"
            title="Active users"
            class="sm:col-span-2 md:col-span-7 lg:col-span-8"
            icon-src="/images/user.png"
            :analytic-data="contact.analytics.user.actived"
          />
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-4 md:grid-cols-12 gap-4 mt-10">
          <analytics-card
            bg-color="#4dcb7b"
            class="sm:col-span-2 md:col-span-6 lg:col-span-7"
            title="Received messages"
            icon-src="/images/union.png"
            :analytic-data="contact.analytics.message.received"
          />
          <analytics-card
            bg-color="#517bf2"
            class="sm:col-span-2 md:col-span-6 lg:col-span-5"
            title="Sent messages"
            icon-src="/images/sent.png"
            :analytic-data="contact.analytics.message.sent"
          />
        </div>
      </div>
      <div class="w-full xl:w-1/3 order-first mb-10 xl:order-2 xl:m-auto">
        <img class="mx-auto" src="/images/plano.png" />
        <p class="status-title text-center mt-6 text-xl font-medium">
          Status account
        </p>
        <p
          class="status-type text-center mt-2 text-2xl font-semibold capitalize"
        >
          {{ contact.plan }}
        </p>
        <base-button class="mt-12 block mx-auto"> Update account </base-button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import contacts from '@/static/json/data.json'

import { Contact } from '@/types/contact'
import { Component, Vue } from 'nuxt-property-decorator'

@Component({
  filters: {
    date: (str: string) => {
      try {
        return Intl.DateTimeFormat('us-EN').format(new Date(str))
      } catch (error) {
        return 'Invalida Date'
      }
    },
  },
})
export default class DetailsContact extends Vue {
  contact?: Contact = contacts.find(
    (c) => c.shortName === this.$route.params.name
  )
}
</script>

<style lang="scss" scoped>
.contact {
  &-avatar {
    background-color: #dee8ec;
  }

  &-name {
    font-size: 28px;
    color: #56616e;

    & ~ span {
      color: #bcc9d3;
    }
  }

  &-date {
    color: #bcc9d3;
  }
}

.info-card {
  span {
    &.title {
      color: #939da5;
    }

    color: #617078;
  }

  &-avatar {
    &-users {
      background-color: $bg-button;
    }
  }
}

.status {
  &-title {
    color: #9eafbf;
  }

  &-type {
    color: #56616e;
  }
}
</style>
