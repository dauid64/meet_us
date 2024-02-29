<script>
    import Header from "./UI/Header.svelte";
    import MeetUpGrid from './Meetups/MeetupGrid.svelte'

    const meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'In this meetup, we will have some experts that teach you how to code!',
            imageUrl: 'https://dcc.ufmg.br/wp-content/uploads/WhatsApp-Image-2023-08-08-at-09.23.38-1024x576.jpeg',
            address: '27th Nerd Road, 32523 New York',
            contactEmail: 'code@test.com'
        },
        {
            id: 'm2',
            title: 'Swim Together',
            subtitle: 'Let\'s go for some swimming',
            description: 'We will simply swim some rounds!',
            imageUrl: 'https://upload.wikimedia.org/wikipedia/commons/a/a7/40._Schwimmzonen-_und_Mastersmeeting_Enns_2017_100m_Brust_Herren_USC_Traun-9897.jpg',
            address: '27th Swim Road, 32523 California',
            contactEmail: 'swim@test.com'
        },
    ]
</script>

<style>
    main {
        margin-top: 5rem;
    }
</style>


<Header/>

<main>
    <MeetUpGrid {meetups}/>
</main>

