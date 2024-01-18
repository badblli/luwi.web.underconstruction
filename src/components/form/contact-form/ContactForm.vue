<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'

const name = ref('')
const corpName = ref('')
const email = ref('')
const phone = ref('')
const message = ref('')
const subject = ref('')
const modalSmallOpen = ref(false)

async function sendForm() {
  try {
    const apiUrl = 'https://prospot.badblli.dev/api/send-emails'
    const formData = {
      data: {
        name: name.value,
        corpName: corpName.value,
        subject: subject.value,
        email: email.value,
        phone: phone.value,
        message: message.value,
      },
    }

    const response = await axios.post(apiUrl, formData)
    modalSmallOpen.value = true
    console.log('İstek başarılı:', response.data)
    // Clear the form fields after successful submission
    name.value = ''
    corpName.value = ''
    subject.value = ''
    email.value = ''
    phone.value = ''
    message.value = ''

    // Başarılı bir şekilde gönderildiğinde burada işlem yapabilirsiniz,
    // örneğin kullanıcıya bir mesaj gösterebilirsiniz.
  } catch (error) {
    console.error('İstek hatası:', error)
    modalSmallOpen.value = false
    // İstek başarısız olduğunda burada işlem yapabilirsiniz,
    // örneğin kullanıcıya bir hata mesajı gösterebilirsiniz.
  }
}
</script>

<template>
  <div class="contact-form">
    <form @submit.prevent="sendForm">
      <div class="columns is-multiline">
        <div class="column is-6">
          <Field>
            <FieldLabel label=" Name">Name</FieldLabel>
            <Control icon="feather:user">
              <VInput v-model="name" placeholder="Your name" />
            </Control>
          </Field>
        </div>
        <div class="column is-6">
          <Field>
            <FieldLabel label="Corp Name">Corp. Name</FieldLabel>
            <Control icon="feather:home">
              <VInput v-model="corpName" placeholder="Your Corp. name" />
            </Control>
          </Field>
        </div>
        <div class="column is-12">
          <Field>
            <FieldLabel label="Subject">Subject</FieldLabel>
            <Control>
              <VInput v-model="subject" placeholder="Subject" />
            </Control>
          </Field>
        </div>
        <div class="column is-12">
          <Field>
            <FieldLabel label="First Name">Email Address</FieldLabel>
            <Control icon="feather:mail">
              <VInput v-model="email" placeholder="Your mail address" />
            </Control>
          </Field>
        </div>

        <div class="column is-12">
          <Field>
            <FieldLabel label="Phone Number">Phone Number</FieldLabel>
            <Control icon="feather:phone">
              <VInput v-model="phone" placeholder="Your phone number" />
            </Control>
          </Field>
        </div>
        <div class="column is-12">
          <Field>
            <FieldLabel label="Message">Message</FieldLabel>
            <Control>
              <VTextarea
                v-model="message"
                :rows="4"
                placeholder="Write your message..."
              />
            </Control>
          </Field>
        </div>
        <div class="column is-12">
          <Control>
            <Button color="primary" bold raised fullwidth>
              <span>Send Message</span>
            </Button>
          </Control>
        </div>
      </div>
    </form>
  </div>
  <!--Modal-->
  <Modal
    title=""
    :open="modalSmallOpen"
    size="small"
    actions="center"
    noscroll
    @close="modalSmallOpen = false"
  >
    <template #content>
      <PlaceholderSection title="Send Succesfully" subtitle="">
        <!-- <template #image>
          <DarkImage src="/@src/assets/illustrations/features/vr.svg" src-dark="/@src/assets/illustrations/features/vr-dark.svg" alt="dark image" />
        </template> -->
      </PlaceholderSection>
    </template>
    <template #action>
      <Button color="primary" :long="2" raised @click="modalSmallOpen = false">
        ✔️
      </Button>
    </template>
  </Modal>
</template>

<style scoped lang="scss">
.contact-form {
  position: relative;

  .column {
    padding: 0.4rem;
  }
}
</style>
