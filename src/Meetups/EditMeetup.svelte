<script>
    import { createEventDispatcher } from "svelte";
    import TextInput from "../UI/TextInput.svelte";
    import Button from "../UI/Button.svelte";
    import Modal from "../UI/Modal.svelte";
    import { isEmpty, isValidEmail } from "../helpers/validation"

    let title = '';
    let subtitle = '';
    let address = '';
    let email = '';
    let description = '';
    let imageUrl = '';
    let formIsValid = false;

    const dispatch = createEventDispatcher();

    $: titleValid = !isEmpty(title);
    $: descriptionValid = !isEmpty(description);
    $: subtitleValid = !isEmpty(subtitle);
    $: addressValid = !isEmpty(address);
    $: imageUrlValid = !isEmpty(imageUrl);
    $: emailValid = isValidEmail(email);
    $: formIsValid = titleValid && subtitleValid && descriptionValid && addressValid && imageUrlValid && imageUrlValid && emailValid

    function submitForm() {
        dispatch('save', {
            title,
            subtitle,
            address,
            email,
            description,
            imageUrl
        });
    }

    function cancel() {
        dispatch('cancel');
    } 
</script>

<style>
    form {
        width: 100%rem;
    }
</style>

<Modal title="Edit Meetup Data" on:cancel>
    <form on:submit|preventDefault={submitForm}>
        <TextInput id="title" label="Title" value={title} on:input="{(event) => title = event.target.value}" type="text" valid={titleValid} validityMessage="Please enter a valid title."/>
        <TextInput id="subtitle" label="Subtitle" value={subtitle} on:input="{(event) => subtitle = event.target.value}" type="text" valid={subtitleValid} validityMessage="Please enter a valid subtitle."/>
        <TextInput id="address" label="Address" value={address} on:input="{(event) => address = event.target.value}" type="text" valid={addressValid} validityMessage="Please enter a valid address."/>
        <TextInput id="imageUrl" label="Image URL" value={imageUrl} on:input="{(event) => imageUrl = event.target.value}" type="text" valid={imageUrlValid} validityMessage="Please enter a valid image URL."/>
        <TextInput id="email" label="E-mail" value={email} on:input="{(event) => email = event.target.value}" type="email" valid={emailValid} validityMessage="Please enter a valid e-mail."/>
        <TextInput id="description" label="Description" bind:value={description} controlType="textarea" valid={descriptionValid} validityMessage="Please enter a valid description."/>
    </form>
    <div slot="footer">
        <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
        <Button type="button" on:click={submitForm} disabled={!formIsValid} >Save</Button>
    </div>
</Modal>