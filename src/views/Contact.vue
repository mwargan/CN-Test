<template>
<div class="contact">
    <h1>Get in touch</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    <form class="card">
        <div class="card-heading">Contact Form</div>
        <div class="grid-columns">
            <label>Name <span class="required-attribute">*</span>
              <input type="text" name="" value="" v-model="searchTerm">
            </label>
            <label>Email Address <span class="required-attribute">*</span>
              <input type="text" name="" value="" v-model="searchTerm">
            </label>
        </div>
        <label>Message <span class="required-attribute">*</span>
            <textarea name="" rows="5"></textarea>
        </label>
        <button type="button">Send</button>
    </form>
</div>

</template>
