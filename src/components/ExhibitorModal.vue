<!-- This component is for showing the modal that will be shown when an exhibitor item is clicked -->

<template>
    <div class="modal-mask">
        <div class="modal-wrapper">
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
                        <section class="name-section">
                            <h4>{{exhibitor.company_name}}</h4>
                            <div class="exhibitor-button-area">
                                <!-- Conditional Render Message with notif or without notide based on value of messaged in exhibitor -->
                                <a v-if="exhibitor.messaged !== 0" class="message active" title="message" @click="$emit('openMessage', exhibitor.id_exhibitor)">
                                    <div class="icon message-icon"></div>
                                    <p>Messaged</p>
                                </a>
                                <a v-if="exhibitor.messaged === 0" class="message" title="message" @click="$emit('openMessage', exhibitor.id_exhibitor)">
                                    <div class="icon message-icon"></div>
                                    <p>Message</p>
                                </a>

                                <!-- Conditional Render Bookmark based on if bookmark have value in exhibitor or not -->
                                <a v-if="exhibitor.bookmark !== 0" class="bookmark active" title="bookmarked" @click="$emit('bookmark', exhibitor.id_exhibitor)">
                                    <div class="icon bookmark-icon"></div>
                                    <p>Bookmarked</p>
                                </a>
                                <a v-if="exhibitor.bookmark === 0" class="bookmark" title="bookmark" @click="$emit('bookmark', exhibitor.id_exhibitor)">
                                    <div class="icon bookmark-icon"></div>
                                    <p>Bookmark</p>
                                </a>
                            </div>
                        </section>
                        <section>
                            <p>{{exhibitor.company_description}}</p>
                        </section>
                        <!-- Get All Attributes Like Category, Industry, and Country, except SPECIAL_PRODUCT_IMAGES -->
                        <section v-for="attribute in exhibitor.attributes" v-if="Object.keys(attribute)[0] != 'SPECIAL_PRODUCT_IMAGES'">
                            <p>{{Object.keys(attribute)[0]}}</p>
                            <ul class="list-unstyled list-key" v-for="category in attribute">
                                <li v-for="(value,key) in category">
                                    <span v-if="value">{{ key }}</span>
                                </li>
                            </ul>
                        </section>
                        
                    </slot>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
  name: 'ExhibitorModal',
  props: ["showExhibitorModal", "exhibitor"]
}
</script>