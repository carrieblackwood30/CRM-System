<template>
    <div class="p-10">
        <h1 class="font-bold text-2xl mb-10">Customers</h1>
        <div v-if="isLoading">loading...</div>
        <UiTable v-else>

            <UiTableHeader>
                <UiTableRow>
                    <UiTableHead class="w-[150px]">image</UiTableHead>
                    <UiTableHead class="w-[300px]">name</UiTableHead>
                    <UiTableHead class="w-[300px]">email</UiTableHead>
                    <UiTableHead>find us</UiTableHead>
                </UiTableRow>
            </UiTableHeader>

            <UiTableBody>
                <UiTableRow v-for="customer in (customers?.documents as unknown as ICustomer[])" :key="customer.$id">
                    <UiTableCell>
                        <NuxtLink :href="`/customers/edit/${customer.$id}`">
                            <NuxtImg :src="customer.avatar_url" :alt="customer.name" width="50" height="50" class="rounded-full" />
                        </NuxtLink>
                    </UiTableCell>
                    <UiTableCell class="font-medium">{{ customer.name }}</UiTableCell>
                    <UiTableCell>{{ customer.email }}</UiTableCell>
                    <UiTableCell>{{ customer.from_source }}</UiTableCell>
                </UiTableRow>
            </UiTableBody>

        </UITable>
    </div>
</template>

<script lang="ts" setup>
    import { useQuery } from '@tanstack/vue-query';
    import { COLLECTION_CUSTOMERS, DB_ID } from '~/app.constants';
    import type { ICustomer } from '~/types/deals.types';

    useSeoMeta({
        title: 'Customers | CRM SYSTEM'
    })

    const { data: customers, isLoading } = useQuery({
        queryKey: ['customers'],
        queryFn: () => DB.listDocuments(DB_ID, COLLECTION_CUSTOMERS)
    })

</script>