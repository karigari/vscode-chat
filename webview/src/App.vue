<template>
    <div id="app" v-bind:style="cssProps">
        <div class="vue-container">
            <messages-section
                v-bind:messages="messages"
                v-bind:users="users">
            </messages-section>

            <form-section
                ref="formSection"
                v-bind:channel="channel"
                v-bind:users="users"
                v-bind:atMentions="atMentions"
                v-bind:status="statusText">
            </form-section>
        </div>
    </div>
</template>

<script>
import Vue from 'vue';
import MessagesSection from './components/MessagesSection.vue';
import FormSection from './components/FormSection.vue'

export default {
    name: 'app',
    props: ['data'],
    components: {
        MessagesSection,
        FormSection
    },
    computed: {
        messages: function() { return this.data ? this.data.messages : []; },
        users: function() { return this.data ? this.data.users : {}; },
        channel: function() { return this.data ? this.data.channel : {} },
        statusText: function() { return this.data ? this.data.statusText : ``; },
        atMentions: function() { return this.data ? this.data.atMentions : []; },
        cssProps() {
            return {
                '--chat-code-font-family': this.data ? this.data.fontFamily : `monospace`,
                '--chat-font-size': this.data ? `${this.data.fontSize}px` : `12px`
            }
        }
    },
}
</script>

<style>
html,
body,
#app {
    height: 100%;
    font-size: var(--chat-font-size);
}

code {
    font-family: var(--chat-code-font-family);
}

.vue-container {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    height: 100%;
    overflow: hidden;
}

.messages-section {
    overflow: auto;
}

.date-heading {
    color: var(--vscode-sideBar-foreground);
    font-weight: normal;
}

.timestamp {
    color: var(--vscode-sideBar-foreground);
}

.message-group {
    display: flex;
    margin: 10px 1px;
}

.message-group-image {
    width: 36px;
    height: 36px;
    margin: 5px 10px 5px 0;
    flex-shrink: 0;
}

.message-group-image img {
    min-width: 100%;
    min-height: 100%;
    border-radius: 2px;
}

.message-group-content {
    width: 100%;
}

.message-list {
    list-style: none;
    padding: 0;
    margin: 5px 0;
}

.message-list li {
    margin: 3px 0;
    word-break: break-word;
}

/* Reactions */
ul.message-reactions {
    list-style: none;
    padding-left: 0;
}

ul.message-reactions li {
    display: inline-block;
    font-size: smaller;
    padding: 2px 5px;
    margin-right: 4px;
    background-color: var(--vscode-input-background);
    border-radius: 3px;
    border: 1px solid var(--vscode-sideBar-background);
}

ul.message-reactions li div {
    display: inline-block;
}

ul.message-reactions li div:first-child {
    margin-right: 3px;
}

/* Form section styles */
.form-section {
    margin-bottom: 10px;
}

.status-text {
    font-size: x-small;
    padding-top: 2px;
}

.status-text:empty::after {
    /* We want to set a min-height, but the font-size is variable */
    /* Source: https://stackoverflow.com/a/33298969 */
    content: ".";
    visibility: hidden;
}

/* At mentions styles */
div.at-mentions {
    background: red;
}

/* Message content styles */
div.msg-author {
    margin: 3px 0;
}

div.msg-title {
    margin: 3px 0;
    font-weight: bold;
}

div.msg-author img {
    max-width: 18px;
    max-height: 18px;
    display: inline-block;
    vertical-align: middle;
}

div.msg-author span {
    display: inline-block;
    vertical-align: middle;
}

div.msg-footer {
    margin-top: 5px;
    font-size: x-small;
}

div.msg-title a,
div.msg-footer a {
    text-decoration: none;
}

div.msg-title a:hover,
div.msg-footer a:hover {
    text-decoration: underline;
}

/* Markdown styles */
.message-list li p {
    -webkit-margin-after: 0;
    -webkit-margin-before: 0;
    line-height: 1.5;
}

.message-list li div.md {
    display: inline;
}

.message-list li code {
    background-color: var(--vscode-editor-selectionHighlightBackground);
    color: var(--vscode-editor-foreground);
}

.message-list li pre {
    padding: 3px;
    background-color: var(--vscode-editor-selectionHighlightBackground);
    border-radius: 2px;
}

.message-list li pre code {
    background-color: transparent;
    white-space: pre-wrap;
}

.message-list li span.edited {
    font-size: x-small;
    color: var(--vscode-scrollbarSlider-activeBackground);
}

.message-list li div.li-line {
    margin: 7px 0;
    border-left: 3px solid white;
    padding-left: 7px;
}

/* Thread replies */
.replies-container {
    margin: 7px 0;
    padding: 4px;
    min-height: 27px;
    background-color: var(--vscode-editor-selectionHighlightBackground);
}

.replies-summary {
    display: flex;
    align-items: center;
}

.replies-summary div {
    margin-right: 5px;
}

.reply-image {
    margin: 0 3px;
}

ul.replies {
    margin: 5px 0;
}

ul.replies li {
    list-style: none;
    margin: 7px 0;
}

.unread {
    border-right: 3px solid var(--vscode-gitDecoration-modifiedResourceForeground);
    padding-right: 5px;
}

.pointer {
    cursor: pointer;
}
</style>
