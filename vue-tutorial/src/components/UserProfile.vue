<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{user.username}}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
      <form class="user-profile__create-twoot">
        <label for="newTwoot">
          <strong>New Twoot</strong>
        </label>
        <textarea v-model="newTwootContent" name="" id="newTwoot" cols="30" rows="10"></textarea>

        <div class="user-porfile__create-twoot-type">
          <label for="newTwootType">
            <strong>Type: </strong>
          </label>
          <select v-model="selectedTwootType" name="" id="newTwootType">
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
      </form>
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>
<script>
import TwootItem from './TwootItem'

export default {
  name: "UserProfile",
  components: { TwootItem }  ,
  data() {
    return {
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant' }
      ],
      followers: 0,
      user: {
        id: 1,
        username: 'thiendang',
        firstname: 'thien',
        lastname: 'dang',
        email: 'thiendang@gmail.com',
        isAdmin: true,
        twoots: [
          { id: 1, content: "Twitter is Amazing!"},
          { id: 2, content: "Hello foo, bar"},
        ]
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`
    }
  },
  methods: {
    followUser() {
      this.followers++
    },
    toggleFavourite(id) {
      console.log(`Favourite Tweet #${id}`)
    }
  },
  mounted() {
    this.followUser()
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

h1 {
  margin: 0;
}

.user-profile__admin-badge {
  background-color: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

.user-profile__create-twoot {
  padding-top: 20px;
  display: flex;
  flex-direction: column;
}

</style>
