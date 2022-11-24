<template>
  <main>
    <CallSection />
    <UserData :userData="userData" />
    <NotficationSettings :notifytype ="userData.notifytypestring" :email.sync="userData.email"/>
    <OtherSettings @sendForm="sendForm" />
  </main>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'IndexPage',

  data(){
    return{
      userData:{}
    }
  },

  methods:{
    ...mapActions({
      loginUser:'login',
      updateUserData:'updateUser'
    }),

    copyUserData(){
      this.userData = JSON.parse(JSON.stringify(this.getUser))
    },
   async sendForm(){

      await this.updateUserData({id:this.userData.id, body:this.userData})
    }
  },

  computed:{
    ...mapGetters({
      getUser:'getUser'
    })
  },

 async mounted(){
  await this.loginUser()
  this.copyUserData()
  }
}
</script>
