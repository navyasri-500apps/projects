<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <!-- Add project button -->
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          Projects
        </h1>
        <p class="mt-2 text-sm text-gray-700">
          A list of all the projects including name, category.
        </p>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          type="button"
          class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          @click="showSidebar"
        >
          Add Project
        </button>
      </div>
    </div>

    <!-- Prjects display table -->
    <CollectionsList
      :projects="projects"
      @edit="edit"
      :headers="headers"
      @deleteRecord="deleteRecord"
    />
    <!-- Prjects display table -->

    <!-- Add or edit project sidebar -->
    <div v-if="openSidebar">
      <CollectionsAdd
        @closeModel="openSidebar = false"
        @save="saveProject"
        :selectedProject="selectedProject"
      />
    </div>
    <!-- Add or edit project sidebar -->
  </div>
</template>

<script setup lang="ts">
const headers = [
  "name",
  "category",
  "status",
  "approve status",
  "total project area",
];
const selectedProject = ref({
  name: "",
  status: "",
  category: "Residential",
  listing_type_name: "",
  total_project_area: "",
  rera_approved: false,
});
const projectIndex = ref(0);
const openSidebar = ref(false);
const url = useAppConfig().projectGetURL;
const serverUrl = useAppConfig().serverProjectURL;
const { pending, data: projects } = await useAuthLazyFetch(url);

const showSidebar = () => {
  openSidebar.value = true;
};

// Insert or update records
const saveProject = async (data: Object) => {
  console.log("data", data);

  // Set options data
  let options = {
    method: `${data.uid} ? 'PUT' :'POST'`,
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
      Authorization:
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzljMGM3MjkzMWI0NGZjOWE1NTc5ZWMyOTg4NzVlYzMiLCJkIjoiMTY4MDA2MiIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNjczNzl9.3_zIDyeZ0ACxOF0VpywmxGpzdhUadzmvMRggb106s5E",
    },
    body: JSON.stringify(data),
  };

  const { data: addTemplateData } = data.uid
    ? await useAuthLazyFetchPut(`${serverUrl}${data.uid}`, options)
    : await useAuthLazyFetchPost(`${serverUrl}`, options);

  // Unshift record into an array to display data
  data.uid
    ? (projects.value[`${projectIndex.value}`] = data)
    : projects.value.unshift(addTemplateData._rawValue);

  // Empty form data
  selectedProject.value = {
    name: "",
    status: "",
    category: "Residential",
    listing_type_name: "",
    total_project_area: "",
    rera_approved: false,
  };
};

// Listen and emit and open sidebar
const edit = (form: Object, index: Number) => {
  selectedProject.value = { ...form };
  projectIndex.value = index;
  openSidebar.value = true;
};

// Listen emit and delete record
const deleteRecord = async (data: Object, index: Number) => {
  await useAuthLazyFetchDelete(`${serverUrl}${data.uid}`);
  emailTemplates.value.splice(index, 1);
};
</script>
