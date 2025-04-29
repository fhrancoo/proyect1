<script lang="ts">
    const { showModalEdit, closeModal, getAllUsers, user } = $props();

    const handleSubmit = async (event: SubmitEvent) => {
        event.preventDefault();

        const formData = new FormData(event.target as HTMLFormElement);
        const data = Object.fromEntries(formData);

        await fetch(`http://localhost:3000/user/${user?.id}`, {
            method: "PATCH",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(data),
        });

        closeModal("edit");
        await getAllUsers();
    };
</script>

{#if showModalEdit}
    <div
        class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50"
    >
        <div class="bg-white p-6 rounded-md shadow-md w-full max-w-md">
            <h2 class="text-xl font-semibold mb-4 text-center">
                Editar usuario.
            </h2>
            <form onsubmit={handleSubmit} class="space-y-4">
                <div>
                    <label
                        for="name"
                        class="block text-gray-700 text-sm font-bold mb-2"
                        >Nombre:</label
                    >
                    <input
                        type="text"
                        id="name"
                        name="name"
                        value={user?.name}
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    />
                </div>

                <div>
                    <label
                        for="email"
                        class="block text-gray-700 text-sm font-bold mb-2"
                        >Email:</label
                    >
                    <input
                        type="email"
                        id="email"
                        value={user?.email}
                        name="email"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    />
                </div>

                <div class="flex justify-end">
                    <button
                        type="submit"
                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline mr-2 disabled:bg-gray-400 disabled:cursor-not-allowed"
                    >
                        Enviar
                    </button>
                    <button
                        type="button"
                        onclick={() => closeModal("edit")}
                        class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    >
                        Cerrar
                    </button>
                </div>
            </form>
        </div>
    </div>
{/if}
