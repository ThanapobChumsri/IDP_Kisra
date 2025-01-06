<template>
  <div class="flex items-center justify-center">
    <div clsas="text-center">
      <div class="text-2xl font-bold text-[#3D5172] text-center">
        IDP Component Dran and Drop
      </div>
      <DNDIDP
        @test="handleTestEvent"
        class="mt-5"
        :ui-type="style"
        :limitSize="size"
        :typeFile="type"
      />
      <div>
        <div class="text-xl font-bold text-[#3D5172] mt-10">Custom Props</div>
        <div class="flex gap-5">
          <div class="w-1/3">
            <UFormGroup label="size limit">
              <UInput v-model="size" size="xl" />
            </UFormGroup>
          </div>
          <div class="w-1/3">
            <UFormGroup label="style">
              <USelectMenu
                size="xl"
                value-attribute="value"
                option-attribute="label"
                placeholder="Style"
                v-model="style"
                :options="styleList"
                class="w-full"
              />
            </UFormGroup>
          </div>
          <div class="w-1/3">
            <UFormGroup label="type">
              <USelectMenu
                size="xl"
                value-attribute="value"
                option-attribute="label"
                placeholder="Type"
                v-model="type"
                :options="typeList"
                class="w-full"
              />
            </UFormGroup>
          </div>
        </div>
      </div>
      <div class="mt-10">
        <pre v-if="style == '1'">
            File Name: {{ attachment.name }}
            File Size: {{ attachment.size ? ((attachment.size / 1024).toFixed(2) + ' KB') : '' }}
            File Type: {{ attachment.type }}
        </pre>
        <div v-else>
          <pre v-for="item in attachmentList" :key="item.name">
            <UButton
            :ui="{ rounded: 'rounded-full' }"
            class="delete"
            @click="attachmentList.splice(attachmentList.indexOf(item), 1)"
            :padded="false"
            color="gray"
            variant="soft"
            icon="i-heroicons-x-mark-20-solid"
          />
                    File Name: {{ item.name }}
                    File Size: {{ item.size ?((item.size / 1024).toFixed(2) + ' KB') : '' }}
                    File Type: {{ item.type }}
                </pre>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, watch } from 'vue'

const size = ref('3')
const style = ref('1')
const type = ref('image/*')
const styleList = ref([
  {
    label: '1',
    value: '1',
  },
  {
    label: '2',
    value: '2',
  },
])
const typeList = ref([
  {
    label: 'Only Image',
    value: 'image/*',
  },
  {
    label: 'Only PDF',
    value: 'application/pdf',
  },
  {
    label: 'Both',
    value: 'image/*,application/pdf',
  },
])
const attachment = ref({})
const attachmentList = ref([])

function handleTestEvent(data) {
  if (style.value == '1') {
    attachment.value = data
  } else {
    attachmentList.value.push(data)
  }
}
</script>

<style></style>
