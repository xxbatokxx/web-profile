<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { useForm, Head, Link } from '@inertiajs/vue3';

defineProps({
    posts: Array,
});
const form = useForm({});
function destroy(id) {
    if (confirm("Are you sure you want to Delete")) {
        form.delete(route('posts.destroy', id));
    }
}
</script>
<template>
    <Head title="Posts" />
    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">Posts</h2>
        </template>
        <div class="py-12">
            <div class="mx-auto space-y-6 max-w-7xl sm:px-2 lg:px-2">
                <div class="p-4 bg-white shadow sm:p-4 sm:rounded-lg">
                    <Link :href="route('posts.create')" as="button"
                        class="px-4 py-2 mr-2 font-bold text-white bg-blue-500 rounded hover:bg-blue-700">
                    Tambah
                    </Link>
                </div>
                <div class="p-4 bg-white shadow sm:p-8 sm:rounded-lg">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-50">
                            <tr>
                                <th scope="col"
                                    class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase">
                                    No</th>
                                <th scope="col"
                                    class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase">
                                    Judul</th>
                                <th scope="col"
                                    class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase">
                                    Kategori</th>
                                <th scope="col"
                                    class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase">
                                    Konten</th>
                                <th scope="col"
                                    class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase">
                                    Tgl Terbit</th>
                                <th scope="col"
                                    class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase">
                                    Penulis</th>
                                <th scope="col"
                                    class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase">
                                    Aksi</th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-gray-200">
                            <!-- Baris 1 -->
                            <tr v-for="post in posts">
                                <td class="px-6 py-4 whitespace-nowrap">{{ post.id }}</td>
                                <td class="px-6 py-4 whitespace-nowrap">{{ post.judul }}</td>
                                <td class="px-6 py-4 whitespace-nowrap">{{ post.kategori }}</td>
                                <td class="px-6 py-4 whitespace-nowrap">{{ post.konten }}</td>
                                <td class="px-6 py-4 whitespace-nowrap"> {{ post.creted_at }}</td>
                                <td class="px-6 py-4 whitespace-nowrap">{{ post.penulis }}</td>
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <div class="flex items-center">
                                        <a :href="route('posts.edit', post.id)"
                                            class="px-4 py-2 mr-2 font-bold text-white bg-green-500 rounded hover:bg-green-700">Edit
                                        </a>
                                        <button @click="destroy(post.id)" tabIndex="-1" type="button"
                                            className="mx-1 px-4 py-2 text-sm text-white bg-red-500 rounded">Hapus</button>
                                    </div>
                                </td>
                            </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</AuthenticatedLayout></template>