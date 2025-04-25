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

<table class="min-w-full bg-white border border-gray-300 shadow-sm rounded-lg overflow-hidden">
    <thead class="bg-gray-50">
        <tr>
            {#each headers as header}
                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider border-b">{header}</th>
            {/each}
        </tr>
    </thead>
    <tbody class="bg-white divide-y divide-gray-200">
        {#each data as user}
            <tr class="hover:bg-gray-50 transition-colors duration-200">
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">{user.name}</td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">{user.email}</td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">{user.role}</td>
            </tr>
        {/each}
    </tbody>
</table>
