<script lang="ts">
    import { onMount } from "svelte";
    import Create from "./Create.svelte";
    import Edit from "./Edit.svelte";
    import Delete from "./Delete.svelte";

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

    type ModalType = "create" | "edit" | "delete";

    let headers = $state(["Nombre", "Email", "Rol", "Acciones"]);
    let users = $state([]) as User[];
    let user = $state(null) as User | null;

    onMount(async () => {
        await getAllUsers();
    });

    const getAllUsers = async () => {
        users = await fetch("http://127.0.0.1:3000/user").then((res) =>
            res.json(),
        );
    };

    let showModalCreate = $state(false);
    let showModalEdit = $state(false);
    let showModalDelete = $state(false);

    const openModal = (name: ModalType) => {
        switch (name) {
            case "create":
                showModalCreate = true;
                break;
            case "edit":
                showModalEdit = true;
                break;
            case "delete":
                showModalDelete = true;
                break;
        }
    };

    const closeModal = (name: ModalType) => {
        switch (name) {
            case "create":
                showModalCreate = false;
                break;
            case "edit":
                showModalEdit = false;
                break;
            case "delete":
                showModalDelete = false;
                break;
        }
    };
</script>

<Create {showModalCreate} {closeModal} {getAllUsers} />
<Edit {showModalEdit} {closeModal} {getAllUsers} {user} />
<Delete {showModalDelete} {closeModal} {getAllUsers} {user} />

<button
    onclick={() => openModal("create")}
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
>
    Crear Usuario
</button>

<table
    class="min-w-full bg-white border border-gray-300 shadow-sm rounded-lg overflow-hidden"
>
    <thead class="bg-gray-50">
        <tr>
            {#each headers as header}
                <th
                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider border-b"
                    >{header}</th
                >
            {/each}
        </tr>
    </thead>
    <tbody class="bg-white divide-y divide-gray-200">
        {#each users as item}
            <tr class="hover:bg-gray-50 transition-colors duration-200">
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900"
                    >{item.name}</td
                >
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900"
                    >{item.email}</td
                >
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900"
                    >{item.role}</td
                >
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                    <button
                        onclick={() => {
                            user = item;
                            openModal("edit");
                        }}
                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    >
                        Editar
                    </button>
                    <button
                        onclick={() => {
                            user = item;
                            openModal("delete");
                        }}
                        class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    >
                        Eliminar
                    </button>
                </td>
            </tr>
        {/each}
    </tbody>
</table>
