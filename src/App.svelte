<script>
    import Header from "./UI/Header.svelte";
    import MeetUpGrid from './Meetups/MeetupGrid.svelte';
    import TextInput from "./UI/TextInput.svelte";
    import Button from "./UI/Button.svelte";

    let title = '';
    let subtitle = '';
    let address = '';
    let email = '';
    let description = '';
    let imageUrl = '';


    let meetups = [
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

    function addMeetUp() {
        const newMeetUp = {
            id: Math.random().toString(),
            title,
            subtitle,
            description,
            imageUrl,
            address,
            contactEmail: email
        };

        meetups = [...meetups, newMeetUp]
    }
</script>

<style>
    main {
        margin-top: 5rem;
    }

    form {
        width: 30rem;
        max-width: 90%;
        margin: auto;
    }
</style>


<Header/>

<main>
    <form on:submit|preventDefault="{addMeetUp}">
        <TextInput id="title" label="Title" value={title} on:input="{(event) => title = event.target.value}" type="text"/>
        <TextInput id="subtitle" label="Subtitle" value={subtitle} on:input="{(event) => subtitle = event.target.value}" type="text"/>
        <TextInput id="address" label="Address" value={address} on:input="{(event) => address = event.target.value}" type="text"/>
        <TextInput id="imageUrl" label="Image URL" value={imageUrl} on:input="{(event) => imageUrl = event.target.value}" type="text"/>
        <TextInput id="email" label="E-mail" value={email} on:input="{(event) => email = event.target.value}" type="email"/>
        <TextInput id="description" label="Description" value={description} on:input="{(event) => description = event.target.value}" controlType="textarea"/>
        <Button type="submit" caption="Save"/>
    </form>
    <MeetUpGrid {meetups}/>
</main>

