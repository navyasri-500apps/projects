<template>
  <!-- Display Projects -->
  <div class="mt-8 flow-root">
    <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
        <div
          class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg"
        >
          <table class="min-w-full divide-y divide-gray-300">
            <thead class="bg-gray-50">
              <tr>
                <th
                  scope="col"
                  class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
                  v-for="(header, index) in headers"
                  :key="index"
                >
                  {{ header }}
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200 bg-white">
              <tr v-for="(project, index) in projects" :key="index">
                <td
                  class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
                >
                  {{ project.name }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ project.category }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ project.status }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ project.approve_status }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ project.total_project_area }}
                </td>
                <!-- Edit/ Delete buttons -->
                <td
                  class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6"
                >
                  <span
                    href="#"
                    class="text-indigo-600 hover:text-indigo-900 cursor-pointer"
                    @click="emit('edit', project, index)"
                    >Edit</span
                  >
                  <span
                    href="#"
                    class="text-indigo-600 hover:text-red-900 ml-4 cursor-pointer"
                    @click="showDeleteModal = true"
                    >Delete</span
                  >
                </td>
                <!-- Edit/ Delete buttons -->
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <!-- Display Projects -->

    <!-- Delete confirmation modal -->
    <TransitionRoot as="template" :show="showDeleteModal">
      <Dialog as="div" class="relative z-10" @close="showDeleteModal = false">
        <TransitionChild
          as="template"
          enter="ease-out duration-300"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="ease-in duration-200"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <div
            class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
          />
        </TransitionChild>

        <div class="fixed inset-0 z-10 overflow-y-auto">
          <div
            class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
          >
            <TransitionChild
              as="template"
              enter="ease-out duration-300"
              enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
              enter-to="opacity-100 translate-y-0 sm:scale-100"
              leave="ease-in duration-200"
              leave-from="opacity-100 translate-y-0 sm:scale-100"
              leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            >
              <DialogPanel
                class="relative transform overflow-hidden rounded-lg bg-white px-4 pt-5 pb-4 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
              >
                <div>
                  <div
                    class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-red-100"
                  >
                    <TrashIcon
                      class="h-6 w-6 text-red-600"
                      aria-hidden="true"
                    />
                  </div>
                  <div class="mt-3 text-center sm:mt-5">
                    <DialogTitle
                      as="h3"
                      class="text-base font-semibold leading-6 text-gray-900"
                      >Are you sure</DialogTitle
                    >
                    <div class="mt-2">
                      <p class="text-sm text-gray-500">
                        Are you sure you want to delete project
                      </p>
                    </div>
                  </div>
                </div>
                <div
                  class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
                >
                  <button
                    type="button"
                    class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                    @click="
                      emit('deleteRecord', selectedProject, projectIndex),
                        (showDeleteModal = false)
                    "
                  >
                    Delete
                  </button>
                  <button
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    @click="showDeleteModal = false"
                    ref="cancelButtonRef"
                  >
                    Cancel
                  </button>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
    <!-- Delete confirmation modal -->
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from "vue";
import { TrashIcon } from "@heroicons/vue/24/outline";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
const props = defineProps({
  headers: Array,
  projects: Array,
});
const emit = defineEmits(["edit", "deleteRecord"]);
const showDeleteModal = ref(false);
const selectedProject = ref({});
const projectIndex = ref(0);
</script>

<style scoped></style>
