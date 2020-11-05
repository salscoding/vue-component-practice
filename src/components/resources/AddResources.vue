<template>
<base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #message>
        <p>Opps, one or more input value is empty!</p>
        <p>Please check all the input field and add some value</p>
    </template>
    <template #actions>
        <base-button @click="confirmError">Got it</base-button>
    </template>
</base-dialog>
<base-card>
    <form @submit.prevent="submitData">
        <div class="form-control">
            <label for="title">Title</label>
            <input id="title" name="title" type="text" ref="titleInput" />
        </div>
        <div class="form-control">
            <label for="discription">Discription</label>
            <textarea id="discription" name="discription" rows="3" ref="discInput"></textarea>
        </div>
        <div class="form-control">
            <label for="link">Link</label>
            <input id="link" name="link" type="url" ref="urlInput" />
        </div>
        <div>
            <base-button type="submit">Add Resource</base-button>
        </div>
    </form>
</base-card>
</template>

<script>
export default {
    inject: ["addResource"],
    data() {
        return {
            inputIsInvalid: false,
        };
    },
    methods: {
        submitData() {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDisc = this.$refs.discInput.value;
            const enteredLink = this.$refs.urlInput.value;

            if (
                enteredTitle.trim() === "" ||
                enteredDisc.trim() === "" ||
                enteredLink.trim() === ""
            ) {
                this.inputIsInvalid = true;
                return;
            }

            this.addResource(enteredTitle, enteredDisc, enteredLink);
        },
        confirmError() {
            this.inputIsInvalid = false;
        },
    },
};
</script>

<style scoped>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
    margin: 1rem 0;
}
</style>
