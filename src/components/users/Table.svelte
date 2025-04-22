<script lang="ts">
    import { onMount } from "svelte";

    interface User {
        id: number;
        name: string;
        email: string;
        role: string;
        profile: Profile;
    }

    interface Profile {
        id: number;
        userId: number;
        bio: string;
    }

    let headers = $state(["Nombre", "Email", "Rol"]);
    let data = $state([]) as User[];

    onMount(async () => {
        data = await fetch("http://127.0.0.1:3000/user").then((res) =>
            res.json(),
        );
    });
</script>

<table>
    <thead>
        <tr>
            {#each headers as header}
                <th>{header}</th>
            {/each}
        </tr>
    </thead>
    <tbody>
        {#each data as user}
            <tr>
                <td>{user.name}</td>
                <td>{user.email}</td>
                <td>{user.role}</td>
            </tr>
        {/each}
    </tbody>
</table>
