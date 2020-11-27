<template>
  <div>
    <page-header/>
    <p> Modal dialog with activator</p>
    <b-modal close-btn size="xs" title="My title" @click:outside="showModal = false">
      <template slot="title" slot-scope="scope">{{scope.title}} {{scope.visible}}</template>
      <template #footer="scope">
        <button class="btn btn-primary" @click="scope.close">Close</button>
      </template>
      Modal with activator
      <template #activator="{on}">
        <button class="btn btn-primary" @click="on">Open</button>
      </template>
    </b-modal>
    <hr>
    <p> Modal dialog with model</p>
    <b-modal v-model="showModal" close-btn size="xs" title="My title" @click:outside="showModal = false">
      Modal with model
    </b-modal>
    <button type="button" class="btn btn-primary" @click="showModal = !showModal">
      Launch demo modal
    </button>
    <hr>
    
    <b-alert :show="dismissCountDown" variant="warning" dismissible @start="showDismissableAlert" @close="closeDismissableAlert" @dismiss-countdown="countDownChanged">
      This alert will dismiss after {{ dismissCountDown }} seconds...
      <template #activator="{on}">
        <button type="button" class="btn btn-primary" @click="on">
          Launch alert
        </button>
      </template>
    </b-alert>

  </div>
</template>

<script>
  import BModal from "../../components/bootstrap/BModal";
  import BAlert from "../../components/bootstrap/BAlert";
  import PageHeader from "./PageHeader";

  export default {
    name: "Home",
    components: {PageHeader, BModal, BAlert},
    data() {
      return {
        showModal: false,
        dismissSecs: 5,
        dismissCountDown: 0,
      }
    },
    methods:{
      showDismissableAlert(){
        this.dismissCountDown = this.dismissSecs;
      },
      closeDismissableAlert(){
        this.dismissCountDown = 0;
      },
      countDownChanged(newDismissCountdown){
        this.dismissCountDown = newDismissCountdown;
      }
    }
  }
</script>

