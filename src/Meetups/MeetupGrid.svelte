<script>
    import MeetUpItem from './MeetupItem.svelte';

    export let meetups;
</script>

<style>
    section {
        width: 100%;
        display: grid;
        grid-template-columns: 1fr;
        grid-gap: 1rem;
    }

    @media (min-width: 768px) {
        section {
            grid-template-columns: repeat(2, 1fr);
        }
    }
</style>

<section id="meetups">
    {#each meetups as meetup}
        <MeetUpItem 
            id={meetup.id}
            title={meetup.title} 
            subtitle={meetup.subtitle} 
            imageUrl={meetup.imageUrl}
            description={meetup.description}
            email={meetup.contactEmail}
            address={meetup.address}
            isFav={meetup.isFavorite}
            on:toggleFavorite
        />
    {/each}
</section>