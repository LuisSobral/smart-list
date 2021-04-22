<template>
  <div class="container mx-auto px-4">
    <div class="grid grid-cols-1 lg:grid-cols-3">
      <h1 class="text-gray-700 text-3xl font-bold">My Contacts List</h1>
      <div class="text-center lg:col-span-2 lg:text-right">
        <input
          v-model="searchName"
          type="text"
          class="w-full my-6 lg:w-2/5 lg:my-0"
          placeholder="Search"
        />
        <base-button
          @click="
            orderedCreation = false
            orderedName = !orderedName
          "
        >
          Order by name
          <span v-if="orderedName" class="ml-1 hidden sm:inline-block"
            >&#128077;</span
          >
        </base-button>
        <base-button
          @click="
            orderedName = false
            orderedCreation = !orderedCreation
          "
        >
          Order by creation
          <span v-if="orderedCreation" class="ml-1 hidden sm:inline-block"
            >&#128077;</span
          >
        </base-button>
        <img
          class="inline cursor-pointer mt-2 sm:mt-0"
          :src="require('@/static/images/organize-blocks.png')"
          @click="listType = 'vertical'"
        />
        <img
          class="inline cursor-pointer mt-2 sm:mt-0"
          :src="require('@/static/images/organize-list.png')"
          @click="listType = 'horizontal'"
        />
      </div>
    </div>
    <h2 class="mt-8 mb-5 text-4xl font-bold">Favorities</h2>
    <list-cards
      is-favorite
      :items="orderedFavorites"
      :empty-text="searchName ? 'No favorite found' : 'No favorite selected'"
      :type="listType"
      @favorite="favorite"
    />
    <hr class="my-8 border-gray-300" />
    <list-cards
      empty-text="No contact found"
      :items="orderedContacts"
      :type="listType"
      @favorite="favorite"
    />
  </div>
</template>

<script lang="ts">
import contacts from '@/static/json/data.json'

import { Contact } from '@/types/contact'
import { Component, Vue } from 'nuxt-property-decorator'

@Component
export default class ListContacts extends Vue {
  // DATA
  favorites: Contact[] = []
  contacts: Contact[] = contacts

  searchName: string = ''
  orderedName: boolean = false
  orderedCreation: boolean = false
  listType: String = 'vertical'

  // COMPUTED
  get contactsSearch(): Contact[] {
    return this.searchName
      ? this.contacts.filter((contact) =>
          contact.name.toLowerCase().includes(this.searchName.toLowerCase())
        )
      : this.contacts
  }

  get orderedContacts(): Contact[] {
    if (this.orderedName) {
      return this.orderName(this.contactsSearch)
    } else if (this.orderedCreation) {
      return this.orderDate(this.contactsSearch)
    }

    return this.contactsSearch
  }

  get favoritesSearch(): Contact[] {
    return this.searchName
      ? this.favorites.filter((contact) =>
          contact.name.toLowerCase().includes(this.searchName.toLowerCase())
        )
      : this.favorites
  }

  get orderedFavorites(): Contact[] {
    if (this.orderedName) {
      return this.orderName(this.favoritesSearch)
    } else if (this.orderedCreation) {
      return this.orderDate(this.favoritesSearch)
    }

    return this.favoritesSearch
  }

  // METHODS
  favorite(item: Contact): void {
    const isFavorite = this.favorites.some(
      (contact) => contact.shortName === item.shortName
    )

    if (isFavorite) {
      this.contacts.push(item)
      this.favorites = this.favorites.filter(
        (contact) => contact.shortName !== item.shortName
      )
    } else {
      this.favorites.push(item)
      this.contacts = this.contacts.filter(
        (contact) => contact.shortName !== item.shortName
      )
    }
  }

  orderName(items: Contact[]): Contact[] {
    return [...items].sort((a: Contact, b: Contact) =>
      a.name > b.name ? 1 : b.name > a.name ? -1 : 0
    )
  }

  orderDate(items: Contact[]): Contact[] {
    return [...items].sort(
      (a: Contact, b: Contact) =>
        new Date(a.created).getTime() - new Date(b.created).getTime()
    )
  }
}
</script>

<style lang="scss" scoped>
h1 {
  color: #56616e;
}

input {
  padding: 8px 12px;
  border-radius: 8px;
  background-color: white;
  border: 1px solid #d1d5db;

  &:focus {
    outline: none;
  }
}

h2 {
  color: #607b99;
}
</style>
