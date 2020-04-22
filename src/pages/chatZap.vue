<template>
 <q-page class="bg-grey-3 column">
  <div class="WAL bg-grey-3" :style="style">
    <q-layout view="lHh Lpr lFf" class="WAL__layout shadow-3" container>
      <q-header elevated>
        <q-toolbar :class="$q.dark.isActive ? 'bg-grey-10' :'bg-blue-5'">
          <q-btn
            round
            flat
            icon="keyboard_arrow_left"
            @click="leftDrawerOpen = !leftDrawerOpen"
          />
          <q-btn round flat>
            <q-avatar>
              <img :src="currentConversation.avatar">
            </q-avatar>
          </q-btn>

          <span class="q-subtitle-1 q-pl-md">
            {{ currentConversation.person }}
          </span>

          <q-space/>

          <q-btn round flat icon="search" />
          <q-btn round flat>
            <q-icon name="attachment" class="rotate-135" />
          </q-btn>
          <q-btn round flat icon="more_vert">
            <q-menu auto-close :offset="[110, 0]">
              <q-list style="min-width: 150px">
                <q-item clickable>
                  <q-item-section>Ver Contatos</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Bloquear</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Selecionar Mensagem</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Silenciar</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Limpar Conversas</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Apagar Mensagem</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-btn>
        </q-toolbar>
      </q-header>

      <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        bordered
        :breakpoint="500"
      >
        <q-toolbar class="bg-blue-5" :class="$q.dark.isActive ? 'bg-grey-10' :'bg-white'">
          <q-avatar class="cursor-pointer">
            <img src="https://cdn.quasar.dev/app-icons/icon-128x128.png" />
          </q-avatar>

          <q-space />

          <q-btn round flat icon="message" />
          <q-btn round flat icon="more_vert">
            <q-menu auto-close :offset="[110, 8]">
              <q-list style="min-width: 150px">
                <q-item clickable>
                  <q-item-section>Novo Grupo</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Perfil</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Arquivado</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Favorito</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Configurações</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Logout</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-btn>

          <q-btn
            round
            flat
            icon="close"
            @click="leftDrawerOpen = false"
          />
        </q-toolbar>

        <q-toolbar class="bg-grey-2" :class="$q.dark.isActive ? 'bg-grey-10' :'bg-white'">
          <q-input rounded outlined dense class="WAL__field full-width" v-model="search" placeholder="Pesquise">
            <template slot="prepend">
              <q-icon name="search" />
            </template>
          </q-input>
        </q-toolbar>

        <q-scroll-area style="height: calc(100% - 100px)">
          <q-list>
            <q-item
              v-for="(conversation, index) in conversations"
              :key="conversation.id"
              clickable
              v-ripple
              @click="currentConversationIndex = index"
            >
              <q-item-section avatar>
                <q-avatar>
                  <img :src="conversation.avatar">
                </q-avatar>
              </q-item-section>

              <q-item-section>
                <q-item-label lines="1">
                  {{ conversation.person }}
                </q-item-label>
                <q-item-label class="conversation__summary" caption>
                  <q-icon name="check" v-if="conversation.sent" />
                  <q-icon name="not_interested" v-if="conversation.deleted" />
                  {{ conversation.caption }}
                </q-item-label>
              </q-item-section>

              <q-item-section side>
                <q-item-label caption>
                  {{ conversation.time }}
                </q-item-label>
                <q-icon name="keyboard_arrow_down" />
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>
      </q-drawer>

      <q-page-container class="bg-blue-2">
        <router-view />
      </q-page-container>

      <q-footer>
        <q-toolbar class="bg-grey-4 text-black row" :class="$q.dark.isActive ? 'bg-grey-10' :'bg-white'">
          <q-btn round flat icon="insert_emoticon" class="q-mr-sm" />
          <q-input rounded outlined dense class="WAL__field col-grow q-mr-sm" bg-color="white" v-model="message" placeholder="Digite sua mensagem" />
          <q-btn round flat icon="mic" />
        </q-toolbar>
      </q-footer>
    </q-layout>
  </div>
  </q-page>
</template>

<script>
export default {
  name: 'WhatsappLayout',
  data () {
    return {
      leftDrawerOpen: false,
      search: '',
      message: '',
      currentConversationIndex: 0,
      conversations: [
        {
          id: 1,
          person: 'Ivan Augusto',
          avatar: 'https://cdn.quasar.dev/team/razvan_stoenescu.jpeg',
          caption: 'Delivery Farm é top',
          time: '15:00',
          sent: true
        },
        {
          id: 2,
          person: 'Giovanne',
          avatar: 'https://cdn.quasar.dev/team/dan_popescu.jpg',
          caption: 'Corona Vairus',
          time: '16:00',
          sent: true
        },
        {
          id: 3,
          person: 'Jonata',
          avatar: 'https://cdn.quasar.dev/team/jeff_galbraith.jpg',
          caption: 'Lucas vacilao',
          time: '18:00',
          sent: true
        },
        {
          id: 4,
          person: 'Rodrigo Paiva',
          avatar: 'https://cdn.quasar.dev/team/allan_gaunt.png',
          caption: 'Bananas',
          time: '17:00',
          sent: true
        }
      ]
    }
  },
  computed: {
    currentConversation () {
      return this.conversations[this.currentConversationIndex]
    },
    style () {
      return {
        height: this.$q.screen.height + 'px'
      }
    }
  }
}
</script>

<style lang="sass">
.q-toolbar
  border-style: none
.WAL
  width: 100%
  height: 80%
  padding-top: 20px
  padding-bottom: 20px
  &:before
    content: ''
    height: 127px
    position: relative
    top: 0
    width: 100%
    background-color: #009688
  &__layout
    margin: auto
    height: 70%
    width: 90%
    border-radius: 5px
  &__field.q-field--outlined .q-field__control:before
    border: none
  .q-drawer--standard
    .WAL__drawer-close
      display: none
@media (max-width: 850px)
  .WAL
    padding: 0
    &__layout
      width: 100%
      border-radius: 0
@media (min-width: 691px)
  .WAL
    &__drawer-open
      display: none
.conversation__summary
  margin-top: 4px
.conversation__more
  margin-top: 0!important
  font-size: 1.4rem
</style>
