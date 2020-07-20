<template>
    <div class="navbar">
      <div>
        <p class="premiumUser" v-if="premium">Premium User</p>
        
        <button v-if="premium"
        class="logOutButton"
        @click="logout()"
        >log out
        </button>

        <button v-if="!premium"
        class="logInButton"
        @click="login()"
        >log in
        </button>
      </div>
        <div class="cart">
          <p>Cart: {{cart.length}}</p>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
          cart: {
            type: Array,
            required: true
          },
          premium: {
            type: Boolean,
            required: true
          }
        },
        methods: {
          logout() {
            this.$emit('log-out', false)
          },
          login() {
            this.$emit('log-in', true)
          }
        }
    }
</script>

<style lang="scss" scoped>
$navbar-color: linear-gradient(-90deg, #84CF6A, #16C0B0);

.navbar {
    background: $navbar-color;
    height: 60px;
    margin-bottom: 15px;
}

.cart {
    margin-right: 25px;
    float: right;
    padding: 5px 20px;
  }

.premiumUser {
    margin-left: 25px;
    float: left;
    padding: 5px 20px;
}

.logOutButton {
    margin:10px;
    float: left;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
}

.logInButton {
    margin:10px;
    float: left;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
}

</style>