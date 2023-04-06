<template>
  <TransitionRoot as="template" :show="open">
    <Dialog
      as="div"
      class="relative z-10"
      @close="(open = false), emit('closeModel')"
    >
      <div class="fixed inset-0" />

      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div
            class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16"
          >
            <TransitionChild
              as="template"
              enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full"
              enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700"
              leave-from="translate-x-0"
              leave-to="translate-x-full"
            >
              <DialogPanel class="pointer-events-auto w-screen max-w-2xl">
                <form
                  class="flex h-full flex-col overflow-y-scroll bg-white shadow-xl"
                >
                  <div class="flex-1">
                    <!-- Header -->
                    <div class="bg-gray-50 px-4 py-6 sm:px-6">
                      <div class="flex items-start justify-between space-x-3">
                        <div class="space-y-1">
                          <DialogTitle
                            class="text-base font-semibold leading-6 text-gray-900"
                            >{{
                              selectedProject.name ? "Edit" : "Add"
                            }}
                            project</DialogTitle
                          >
                          <p class="text-sm text-gray-500">
                            Get started by filling in the information below to
                            create your new project.
                          </p>
                        </div>
                        <div class="flex h-7 items-center">
                          <button
                            type="button"
                            class="text-gray-400 hover:text-gray-500"
                            @click="(open = false), emit('closeModel')"
                          >
                            <span class="sr-only">Close panel</span>
                            <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                          </button>
                        </div>
                      </div>
                    </div>

                    <!-- Divider container -->
                    <div
                      class="space-y-6 py-6 sm:space-y-0 sm:divide-y sm:divide-gray-200 sm:py-0"
                    >
                      <!-- Project Name -->
                      <div
                        class="space-y-2 px-4 sm:grid sm:grid-cols-3 sm:gap-4 sm:space-y-0 sm:px-6 sm:py-5"
                      >
                        <div>
                          <label
                            for="project-name"
                            class="block text-sm font-medium leading-6 text-gray-900 sm:mt-1.5"
                            >Project name</label
                          >
                        </div>
                        <div class="sm:col-span-2">
                          <input
                            type="text"
                            name="project-name"
                            id="project-name"
                            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            v-model="selectedProject.name"
                          />
                        </div>
                      </div>
                      <!-- Project Name -->

                      <!-- Project status -->
                      <div
                        class="space-y-2 px-4 sm:grid sm:grid-cols-3 sm:gap-4 sm:space-y-0 sm:px-6 sm:py-5"
                      >
                        <div>
                          <label
                            for="project-name"
                            class="block text-sm font-medium leading-6 text-gray-900 sm:mt-1.5"
                            >status</label
                          >
                        </div>
                        <div class="sm:col-span-2">
                          <input
                            type="text"
                            name="project-name"
                            id="project-name"
                            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            v-model="selectedProject.status"
                          />
                        </div>
                      </div>
                      <!-- Project Name -->

                      <!-- Project category -->

                      <div
                        class="space-y-2 px-4 sm:grid sm:grid-cols-3 sm:gap-4 sm:space-y-0 sm:px-6 sm:py-5"
                      >
                        <label
                          for="category"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Category</label
                        >
                        <select
                          id="category"
                          name="category"
                          class="sm:col-span-2mt-2 block w-full rounded-md border-0 py-1.5 pl-3 pr-10 text-gray-900 ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-indigo-600 sm:text-sm sm:leading-6"
                          v-model="selectedProject.category"
                        >
                          <option selected="Residential">Residential</option>
                          <option selected="Commercial">Commercial</option>
                        </select>
                      </div>

                      <!-- Project category -->

                      <!--Project Type -->

                      <div
                        class="space-y-2 px-4 sm:grid sm:grid-cols-3 sm:gap-4 sm:space-y-0 sm:px-6 sm:py-5"
                      >
                        <div>
                          <label
                            for="project-name"
                            class="block text-sm font-medium leading-6 text-gray-900 sm:mt-1.5"
                            >Project Type</label
                          >
                        </div>
                        <div class="sm:col-span-2">
                          <input
                            type="text"
                            name="project-name"
                            id="project-name"
                            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            v-model="selectedProject.listing_type_name"
                          />
                        </div>
                      </div>
                      <!-- Total Project Area -->

                      <div
                        class="space-y-2 px-4 sm:grid sm:grid-cols-3 sm:gap-4 sm:space-y-0 sm:px-6 sm:py-5"
                      >
                        <div>
                          <label
                            for="project-name"
                            class="block text-sm font-medium leading-6 text-gray-900 sm:mt-1.5"
                            >Total Project Area</label
                          >
                        </div>
                        <div class="sm:col-span-2">
                          <input
                            type="text"
                            name="project-name"
                            id="project-name"
                            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            v-model="selectedProject.total_project_area"
                          />
                        </div>
                      </div>
                      <!-- rera_approved: "", -->

                      <div class="relative flex items-start">
                        <div class="flex h-6 items-center">
                          <input
                            id="comments"
                            aria-describedby="comments-description"
                            name="comments"
                            type="checkbox"
                            class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-600"
                            v-model="selectedProject.rera_approved"
                          />
                        </div>
                        <div class="ml-3 text-sm leading-6">
                          <label
                            for="comments"
                            class="font-medium text-gray-900"
                            >Rera Approved</label
                          >
                          {{ " " }}
                          <span id="comments-description" class="text-gray-500"
                            ><span class="sr-only">New comments </span>so you
                            always know what's happening.</span
                          >
                        </div>
                      </div>
                    </div>
                  </div>

                  <!-- Action buttons -->
                  <div
                    class="flex-shrink-0 border-t border-gray-200 px-4 py-5 sm:px-6"
                  >
                    <div class="flex justify-end space-x-3">
                      <button
                        type="button"
                        class="rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                        @click="(open = false), emit('closeModel')"
                      >
                        Cancel
                      </button>
                      <button
                        type="submit"
                        class="inline-flex justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                        @click="saveData()"
                      >
                        Save
                      </button>
                    </div>
                  </div>
                </form>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup lang="ts">
import { ref, defineEmits, defineProps } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";
import {
  LinkIcon,
  PlusIcon,
  QuestionMarkCircleIcon,
} from "@heroicons/vue/20/solid";

const selectedValue = ref("Residential");

const emit = defineEmits(["closeModel", "save"]);

const props = defineProps({
  selectedProject: {type: Object, default:() => []},
});
const open = ref(true);

const saveData = () => {
  // Prepare form data to insert or update
  let formData = {
    name: props.selectedProject.name,
    listing_type_name: props.selectedProject.listing_type_name,
    total_project_area: props.selectedProject.total_project_area,
    rera_approved: props.selectedProject.rera_approved,
    satus: props.selectedProject.status,
    category: props.selectedProject.category,
  };

  if (props.selectedProject && props.selectedProject.uid)
    formData["uid"] = props.selectedProject.uid;

  // Emits data to insert or update data
  emit("save", formData);
};
</script>
