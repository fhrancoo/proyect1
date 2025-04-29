<script lang="ts">
    const { showModalDelete, closeModal, getAllUsers, user } = $props();

    const handleSubmit = async (event: SubmitEvent) => {
        event.preventDefault();

        await fetch(`http://localhost:3000/user/${user?.id}`, {
            method: "DELETE",
            headers: {
                "Content-Type": "application/json",
            },
        });

        closeModal("delete");
        await getAllUsers();
    };
</script>

{#if showModalDelete}
    <div
        class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50"
    >
        <div class="bg-white rounded-lg shadow-xl overflow-hidden">
            <div class="px-6 py-4">
                <h2 class="text-xl font-semibold text-gray-800 mb-2">
                    Eliminar Usuario
                </h2>
                <p class="text-gray-700 mb-4">
                    ¿Estás seguro de que quieres eliminar este usuario?
                </p>
                <form onsubmit={handleSubmit} class="flex justify-end gap-2">
                    <button
                        type="submit"
                        class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    >
                        Eliminar
                    </button>
                    <button
                        type="button"
                        onclick={() => closeModal("delete")}
                        class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    >
                        Cancelar
                    </button>
                </form>
            </div>
        </div>
    </div>
{/if}
