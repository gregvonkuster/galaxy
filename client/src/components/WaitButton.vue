/** Button variant with waiting and progress tracking. */
<template>
    <button class="ui-button-default" :class="buttonClass" type="button" @click="$emit('click')">
        <i class="icon fa" :class="iconClass"> </i>
        <span class="title"> {{ currentText }} </span>
        <div class="progress" v-if="percentage != -1">
            <div class="progress-bar" :style="{ width: progressWidth }"></div>
        </div>
    </button>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            default: "",
        },
        icon: {
            type: String,
            default: "fa-play",
        },
        percentage: {
            type: Number,
            default: -1,
        },
        waiting: {
            type: Boolean,
            default: false,
        },
        waitText: {
            type: String,
            default: "Sending...",
        },
        variant: {
            type: String,
            default: "info",
        },
    },
    computed: {
        progressWidth() {
            return `${this.percentage}%`;
        },
        buttonClass() {
            if (this.waiting) {
                return "disabled";
            } else {
                return `btn btn-${this.variant}`;
            }
        },
        iconClass() {
            if (this.waiting) {
                return "fa-spinner fa-spin mr-1";
            } else {
                return this.icon + " mr-1";
            }
        },
        currentText() {
            if (this.waiting) {
                return this.waitText;
            } else {
                return this.title;
            }
        },
    },
};
</script>
