<script>
    import meetups from './Meetups/meetups-store.js'
    import Header from "./UI/Header.svelte";
    import MeetUpGrid from './meetups/MeetupGrid.svelte';
    import EditMeetup from "./meetups/EditMeetup.svelte";
    import Button from "./UI/Button.svelte";

    let editMode;

    function addMeetUp(event) {
        const newMeetUp = {
            id: Math.random().toString(),
            title: event.detail.title,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            imageUrl: event.detail.imageUrl,
            address: event.detail.address,
            contactEmail: event.detail.email
        };

        meetups.addMeetup(newMeetUp);
        editMode = null;
    }

    function toggleFavorite(event) {
        const id = event.detail;
        meetups.toggleFavorite(id);
    }

    function cancelEdit() {
        editMode = null;
    }
</script>

<style>
    main {
        margin-top: 5rem;
    }

    .meetup-controls {
        margin: 1rem;
    }
</style>


<Header/>

<main>
    <div class="meetup-controls">

    </div>
    <Button on:click="{() => editMode = 'add'}">New Meetup</Button>
    {#if editMode === 'add'}
        <EditMeetup on:save="{addMeetUp}" on:cancel={cancelEdit} />
    {/if}
    <MeetUpGrid meetups={$meetups} on:toggleFavorite="{toggleFavorite}"/>
</main>

