<script>
    import Header from "./UI/Header.svelte";
    import MeetUpGrid from './Meetups/MeetupGrid.svelte';
    import EditMeetup from "./Meetups/EditMeetup.svelte";
    import Button from "./UI/Button.svelte";

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'In this meetup, we will have some experts that teach you how to code!',
            imageUrl: 'https://dcc.ufmg.br/wp-content/uploads/WhatsApp-Image-2023-08-08-at-09.23.38-1024x576.jpeg',
            address: '27th Nerd Road, 32523 New York',
            contactEmail: 'code@test.com',
            isFavorite: false,
        },
        {
            id: 'm2',
            title: 'Swim Together',
            subtitle: 'Let\'s go for some swimming',
            description: 'We will simply swim some rounds!',
            imageUrl: 'https://upload.wikimedia.org/wikipedia/commons/a/a7/40._Schwimmzonen-_und_Mastersmeeting_Enns_2017_100m_Brust_Herren_USC_Traun-9897.jpg',
            address: '27th Swim Road, 32523 California',
            contactEmail: 'swim@test.com',
            isFavorite: false,
        },
    ]

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

        meetups = [...meetups, newMeetUp]
    }

    function toggleFavorite(event) {
        const id = event.detail;
        const updatedMeetup = { ...meetups.find(m => m.id === id) };
        updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
        const meetupIndex = meetups.findIndex(m => m.id === id);
        const updatedMeetups = [...meetups];
        updatedMeetups[meetupIndex] = updatedMeetup
        meetups = updatedMeetups
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
    <Button caption="New Meetup" on:click="{() => editMode = 'add'}"/>
    {#if editMode === 'add'}
        <EditMeetup on:save="{addMeetUp}" />
    {/if}
    <MeetUpGrid {meetups} on:toggleFavorite="{toggleFavorite}"/>
</main>

