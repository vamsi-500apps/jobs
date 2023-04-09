<template>
  <div>
    <TransitionRoot as="template" :show="open">
      <Dialog as="div" class="relative z-10" @close="open = false">
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
                  <div
                    class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                  >
                    <div class="px-4 sm:px-6">
                      <div class="items-start justify-between">
                        <DialogTitle
                          class="text-base font-semibold leading-6 text-white-900 mb-5"
                          >Add Candidates</DialogTitle
                        >
                        <hr />
                        <div class="mt-6 py-6">
                          <label />Profile Id
                          <input
                            v-model="profile_id"
                            id="text"
                            class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          />
                          <label />Title
                          <input
                            v-model="title"
                            type="text"
                            class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          />
                          <label for="test-type">Designation</label>
                          <input
                            v-model="designation"
                            id="test-type"
                            class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          />
                          <label />Education Qualification
                          <input
                            v-model="education_qualification"
                            type="text"
                            class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          />
                          <label />Experience
                          <input
                            v-model="experience_level "
                            type="text"
                            class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          />
                          <label />Skills Description
                          <input
                            v-model=" skills_description"
                            type="text"
                            class=" truncate p-4 block w-full  rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
                          />
                        
                        </div>

                        <div class="ml-3 flex h-7 items-center">
                          <button
                            type="button"
                            class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                            @click="open = false"
                          >
                            <span class="sr-only">Close panel</span>
                          </button>
                        </div>
                      </div>
                    </div>
                    <div class="relative flex-1 px-2 sm:px-6">
                      <!-- Your content -->
                      <div class="bg-gray h-auto">
                        <div class="bg-gray-50 mx-auto px-4 py-3">
                          <div class="text-center mb-0 rounded-0">
                            <div class="flex justify-end mr-3 mt-4">
                              <button
                                @click="open = false"
                                type="button"
                                class="border rounded-md bg-white py-2 px-3 text-sm font-semibold text-gray-600 shadow-sm hover:bg-gray-50 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mr-3"
                              >
                                Cancel
                              </button>
                              <button 
                                type="button"
                                class="rounded-md bg-indigo-600 py-2 px-4 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                                @click="postData()"
                              >
                                Save
                              </button>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </div>
</template>
<script setup lang="ts">
import { ref, defineEmits } from "vue";

import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";

const emit = defineEmits(["postBody"]);

let title = ref("");
let designation = ref("");
let education_qualification = ref();
let experience_level = ref("");
let skills_description = ref("");
let profile_id = ref();

const open = ref(true);

//sending body to the emit
const postData = async () => {
  let body =
  {
  title: title.value,
  industries: "string",
  designation: designation.value,
  education_qualification: education_qualification.value,
  skills_description: skills_description.value,
  external_source: "string",
  experience_level: experience_level.value,
  listed_date: "2023-04-09T05:56:28",
  location_id: 0,
  description: "string",
  experience_in_placeof_education: "string",
  expiry_date: "2023-04-09T05:56:28",
  apply_url: "string",
  operation_type: "create",
  work_hours: "string",
  working_days: "string",
  is_work_remote_allowed: 0,
  workplace_type: "onsite",
  employment_status: "ft",
  company_job_code: "string",
  profile_id: profile_id.value,
  state: "closed",
  job_count: 0,
  gender: "male",
  special_commitments: "string",
  security_clearances: "string",
  languages: "string",
  start_date: "2023-04-09T05:56:28",
  job_benefits: "string",
  currency_code: "string",
  salary_incentives: "string",
  salary_high_end: "string",
  salary_low_end: "strin",
  salary_period: "string",
  base_salary: "string",
  show_poster: "yes",
  poster_info: "name",
  listing_type: "basic",
  last_scrapped_date: "2023-04-09T05:56:28",
  is_draft: 0,
  uid: "d62dc20a-13dd-4672-aafb-6679dafb2099",
  id: 1018005,
  created_date: "2023-04-09T05:56:30"
}
  
  emit("postBody", body);
  //open.value=false;
};
</script>