<!-- This component is for showing the modal that will be shown when an Modal item is clicked, also to send the message to the exhibitor -->

<template>
    <div class="modal-mask">
        <div id="message-modal" class="modal-wrapper">
            <div class="modal-container">

                <div class="modal-header">
                    <slot name="header">
                        <button class="modal-default-button" @click="$emit('close')">
                        Back
                        </button>
                    </slot>
                </div>

                <div class="modal-body">
                    <slot name="body">
                        <section v-if="isMessageSubmitted">
                            <h3>Congratulations!</h3>
                            <p>Your message will be sent to the company to revert at their own discretion once approved by the Organiser.</p>
                            <button class="back-button" @click="$emit('close')">Back</button>
                        </section>
                        <section v-if="!isMessageSubmitted">
                            <h3>To: {{exhibitor.company_name}}</h3>
                                <form
                                id="message-form"
                                @submit.prevent="$emit('submitMessage', exhibitor.id_exhibitor)"
                                >
                                    <p>
                                        <label for="email">Email</label>
                                        <input
                                        id="email"
                                        placeholder="Enter your email here..."
                                        type="email"
                                        name="email"
                                        required
                                        >
                                    </p>
                                    <p>
                                        <label for="message">Message</label>
                                        <textarea placeholder="Enter your message here..." id="message" name="message" required></textarea>
                                    </p>
                                    <p>
                                        Include a personal message to reach out to this exhibitor. By sending this message, you must not take part in any canvassing, soliciting, objectionable behavior or be involved in any activity which may disrupt the event. We reserve the right to block your message if your behaviour is deemed unacceptable/unsuitable by the Organiser.
                                        </p>
                                    <p>
                                        <input class="submit-button"
                                        type="submit"
                                        value="Submit"
                                        >
                                        <button class="back-button" @click="$emit('close')">Back</button>
                                    </p>
                                </form>
                                
                        </section>
                    </slot>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
  name: 'MessageModal',
  props: ["showMessageForm", "isMessageSubmitted", "exhibitor"]
}
</script>