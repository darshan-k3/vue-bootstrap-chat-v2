<script>



export default{
  // reactive state

  data(){
    return{
      timer : null,
      count: 0,
      countUsers: 0,
      countConversation : 0,
      countUserMessages : 0,
      userMessage : '',
      chatMessage : '',
      buttonDisabled: false,
      currentConversation: [{id: 0 , convLine: 'Welcome to this front end chat app!'}],
      description : [{id: 0, message : 'Here is the description of people in the conversation!'}],
      userMessages : [{id: 0, message : ''}],

      conversation : ['Hiya how\'s it going!', 'I\'m good thanks', 'What are you doing tonight?',  'Not much', 'Ok fair enough',  ],
      users :['John', 'Jane', 'Bob', 'Mary', 'Steve'],
      ages : [34, 80, 25, 36, 19],
      jobs : ['Chef', 'Retired army veteran', 'Waiter', 'Builder', 'Cartographer'],
      hobbies : ['Hiking', 'Reading', 'Playing Chess', 'Playing the Piano', 'Gardening'],
      hobbiesDescriptions : ['I love to go hiking', 'I love to read', 'I love to play chess', 'I love to play the piano', 'I love to garden'],
  
    }
  },

  computed: {
    generateDescription(){
      this.chatMessage = this.users.slice(this.countUsers, this.countUsers + 1).toString() + "\n" + this.ages.slice(this.countUsers, this.countUsers + 1).toString() + " years old<br></br>" + "Is currently a " + this.jobs.slice(this.countUsers, this.countUsers + 1).toString() + "<br></br>" + this.hobbiesDescriptions.slice(this.countUsers, this.countUsers + 1).toString();
      return chatMessage;
    }

  },
  methods: {
    increment(){
      this.count++;
    },
   
    checkCount(){
      if(this.countConversation < this.conversation.length-1){
        this.countConversation++;
      }else{
        this.countConversation = 0;
      }
      if(this.countUsers < this.users.length-1){
        this.countUsers++;
      }else{
        this.countUsers = 0;
      }
    },

    stop(){
    clearInterval(this.timer);
    },

    clear(){
      this.countConversation = 0;
      this.countUsers = 0;
      this.messages = [];
      this.currentConversation = [];
    },
    

    start(){
      if(this.timer == null){
          this.timer = setInterval(() => {
          this.description.push({id: this.description.length + 1, message : this.users.slice(this.countUsers, this.countUsers + 1).toString() + "\n" + this.ages.slice(this.countUsers, this.countUsers + 1).toString() + " years old\n" + "Is currently a " + this.jobs.slice(this.countUsers, this.countUsers + 1).toString() + "\n" + this.hobbiesDescriptions.slice(this.countUsers, this.countUsers + 1).toString()})
          this.description.shift();
          this.currentConversation.push({id: this.currentConversation.length + 1, convLine : this.users.slice(this.countUsers, this.countUsers + 1) + " - " + this.conversation.slice(this.countConversation, this.countConversation + 1).toString()})
          this.userMessages.push(this.userMessage);
          this.checkCount();
      }, 5000)
      }
    }
    
  },
  mounted(){
    console.log(`The initial count is currently:${this.count}`)
    console.log(`Please enter your message here ${this.userMessage}`)
    window.addEventListener('keyup', function(event) {
      if(event.keyCode === 13){
        if(userMessage !== ''){
        messages.push({id:messages.length + 1, message: userMessage});
        }
      }
    });
  
  },
  
}

</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-md">
        <div class="conversationMain">
           <!--User message displayed at top of screen-->
          <div class="col-md ">
            <p id="conversation" v-for="c in currentConversation">{{c.convLine}}</p>
            <p>&#x1F600</p>
            <p id="newMessage" v-for="m in userMessages">{{m.message}}</p>
          </div>
          <div class="col-md ">
            
          </div>
        </div>
      </div>
    <div class="col-md">
      <div class="row">
        <div class="description">
             <p id="chatMessage" v-for="m in description">{{m.message}}</p>
        </div>
           <div class="row">
      <div class="userArea">
        <input id="userMessage" v-on:keyup.13="description.push({id:description.length + 1, message: userMessage})" v-model="userMessage" placeholder="Join the convo"/>
        <button type="button" :disabled="userMessage === ''" @click="userMessages.push({id:description.length + 1, message: userMessage})" class="btn btn-primary">Send</button>
        <button id="stop" type="button" @click="stop" class="btn btn-danger">Stop</button>
        <button id="clear" type="button" @click="clear" class="btn btn-warning">Clear</button>
        <button id="start" type="button" @click="start" class="btn btn-success">Start</button>
      </div>
    </div> 
      </div>
 
      </div>
    </div>
  </div>
 
</template>

<style>


.container{
  list-style: none;
}
.description{
  white-space: pre-wrap;
  list-style: none;
}



</style>

