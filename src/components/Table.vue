<script setup>
import { ref } from 'vue';
import Rows from './Rows.vue';
import DemoLoginModal from './Modal_Login.vue';
// defineProps({
//   msg: String,
// });

const count = ref(0);
// don't forget to mount to app div

export default {
  name: 'app',
  components: {
    DemoAdaptiveModal,
    DemoDraggableModal,
    DemoResizableModal,
    DemoErrorModal,
    DemoLoginModal,
    DemoDogProfileModal,
    DemoConditionalModal,
    DemoSizeModal,
  },
  data() {
    return {
      canBeShown: false,
    };
  },
  created() {
    setInterval(() => {
      this.canBeShown = !this.canBeShown;
    }, 5000);
  },
  methods: {
    conditionalShow() {
      this.$modal.show('conditional-modal', {
        show: this.canBeShown,
      });
    },
    showBasicDialog() {
      this.$modal.show('dialog', {
        text: 'I am a tiny dialog box.<br/>And I render <b>HTML!</b>',
      });
    },
    showTitleDialog() {
      this.$modal.show('dialog', {
        title: 'Information',
        text: 'Check out, I have a title 😎',
      });
    },
    showButtonsDialog() {
      this.$modal.show('dialog', {
        title: 'The standard Lorem Ipsum passage',
        text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        buttons: [
          {
            title: 'Cancel',
            handler: () => {
              this.$modal.hide('dialog');
            },
          },
          {
            title: 'Like',
            default: true,
            handler: () => {
              alert('Like action');
            },
          },
          {
            title: 'Repost',
            handler: () => {
              alert('Repost action');
            },
          },
        ],
      });
    },
    showDynamicRuntimeModal() {
      this.$modal.show(
        {
          template: `
              <div class="example-modal-content">
                <p>Component has been created inline.</p>
                <p>{{ text }}</p>
                <p>This component is draggable because of the "dynamicDefault" property.</p>
              </div>
            `,
          props: ['text'],
        },
        {
          text: 'Text has been passed as a property.',
        },
        {
          height: 'auto',
        }
      );
    },
    showDynamicComponentModal() {
      this.$modal.show(DemoCustomComponent, {
        text: 'This text is passed as a property',
      });
    },
    showDynamicComponentModalWithModalParams() {
      let counter = 0;
      const interval = setInterval(() => {
        if (counter === 5) {
          clearInterval(interval);
        } else {
          counter++;
        }
        const name = `dynamic-modal-${Math.random()}`;
        this.$modal.show(
          {
            template: `
              <div class="example-modal-content">
                <h2>{{ name }}</h2>
                <button class="btn" @click="closeByName">Close using name</button>
                <button class="btn" @click="closeByEvent">Close using events</button>
                <button class="btn" @click="this.$modal.hideAll">Close all dynamic modals</button>
              </div>
            `,
            props: ['name'],
            methods: {
              closeByName() {
                this.$modal.hide(name);
              },
              closeByEvent() {
                this.$emit('close');
              },
            },
          },
          { name },
          { name, height: 'auto' }
        );
      }, 300);
    },
    dialogEvent(eventName) {
      console.log('Dialog event: ' + eventName);
    },
  },
};
</script>

<template>
  <body>
    <div class="container">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">User Management</h5>
          <button
            type="button"
            class="btn btn-primary"
            @click="$modal.show('demo-login')"
          >
            Add User
          </button>
        </div>
      </div>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
            <th scope="col">Role</th>
            <th scope="col">Status</th>
            <th scope="col">Actions</th>
          </tr>
        </thead>
        <tbody id="userTableBody">
          <Rows
            id="1"
            name="tanmay"
            email="xyz@gmail.com"
            role="director"
            status="Active"
          ></Rows>
        </tbody>
      </table>
    </div>
  </body>
</template>

<style scoped>
a {
  color: #42b983;
}

.card-body {
  background-color: rgb(94, 217, 255);
}
</style>
