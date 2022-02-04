<script setup>
import { computed } from 'vue'
import { useStore } from 'vuex'

import AsideMenuList from '@/components/AsideMenuList.vue'

defineProps({
  menu: {
    type: Array,
    default: () => []
  }
})

const store = useStore()
const isFullScreen = computed(() => store.state.isFullScreen)
const isPropertiesMobileExpanded = computed(() => store.state.isAsideMobileExpanded)
const isAsideLgActive = computed(() => store.state.isAsideLgActive)
const selectedTask = computed(() => store.state.tasks.selectedTask)
const taskMessages = computed(() => store.state.taskmessages.messages)
const taskFiles = computed(() => store.state.taskfiles.files)
const tags = computed(() => store.state.tasks.tags)
const employees = computed(() => store.state.employees.employees)
const projects = computed(() => store.state.projects.projects)
const localization = computed(() => store.state.localization.localization)
const colors = computed(() => store.state.colors.colors)

const statuses = [
  'status_not_begin',
  'status_ready',
  'task_by_link',
  'status_note',
  'status_in_work',
  'status_task_ready',
  'status_paused',
  'status_cancelled',
  'status_reject',
  'status_refine'
]

// const asideLgClose = () => {
//   store.dispatch('asideLgToggle', false)
// }

const menuClick = (event, item) => {
  //
}
</script>

// isPropertiesMobileExpanded ? 'right-0' : '-right-96',

<template>
  <aside
    v-if="selectedTask.name"
    v-show="!isFullScreen"
    id="aside"
    class="-right-96 w-96 fixed top-0 z-40 h-screen bg-white transition-position lg:right-0 dark:border-r dark:border-gray-800 dark:bg-gray-900"
    :class="[ isPropertiesMobileExpanded ? 'right-0' : '-right-90', isAsideLgActive ? 'block' : 'lg:hidden xl:block' ]"
  >
    <!-- <div class="flex flex-row w-full text-dark flex-1 h-14 items-center">
      <nav-bar-item
        type="hidden lg:flex xl:hidden"
        active-color="text-white"
        active
        @click="asideLgClose"
      >
        <icon
          :path="mdiMenu"
          class="cursor-pointer"
          size="24"
        />
      </nav-bar-item>
      <div class="flex-1 px-5">
      </div>
    </div> -->

    <div class="p-3 break-words">
      <div class="user_customer_custom"><svg style="width:24px;height:24px" viewBox="0 0 24 24">
        <path fill="currentColor" d="M20 18V20H13.5C9.91 20 7 17.09 7 13.5V7.83L3.91 10.92L2.5 9.5L8 4L13.5 9.5L12.09 10.91L9 7.83V13.5C9 16 11 18 13.5 18H20Z" />
      </svg> {{ selectedTask.customer_name }}</div>
      <p><strong>{{ selectedTask.name }}</strong></p>

   <!--   <p class="mt-3"><strong>{{ localization.task_created }}:</strong> {{ selectedTask.date_create }}</p>
      <p><strong>Исполнитель:</strong> {{ selectedTask.email_performer }}</p>-->
      <p style="display: none"><strong>{{ localization.gc_status }}: </strong> {{ localization[statuses[selectedTask.status]] }}</p>
      <p v-if="selectedTask.uid_project !== '00000000-0000-0000-0000-000000000000'"><strong>{{ localization.props_prj }}: </strong> {{ projects[selectedTask.uid_project].name }}</p>
      <p v-if="selectedTask.uid_marker !== '00000000-0000-0000-0000-000000000000'"><strong>Цвет:</strong> <span :style="{'background-color': colors[selectedTask.uid_marker].backcolor}" class="p-1">{{ colors[selectedTask.uid_marker].name }}</span></p>
   <!--   <p v-if="selectedTask.plan"><strong>План:</strong> {{ selectedTask.plan }}</p>
      <p v-if="selectedTask.email"><strong>Задача открыта для:</strong> {{ selectedTask.email }}</p>
      <p v-if="selectedTask.checklist"><strong>Чек-лист:</strong> {{ selectedTask.checklist }}</p>
      <p><strong>Задачу создал:</strong> {{ selectedTask.customer_name }}</p>-->

      <div class="mt-3 custom-list-tags" v-if="selectedTask.tags.length">
       <!-- <p class="text-center">{{ localization.Labels }}</p>-->
        <span class="mt-3 tags-custom active">
   <svg style="width:24px;height:24px" viewBox="0 0 24 24">
    <path fill="currentColor" d="M12,4A4,4 0 0,1 16,8A4,4 0 0,1 12,12A4,4 0 0,1 8,8A4,4 0 0,1 12,4M12,6A2,2 0 0,0 10,8A2,2 0 0,0 12,10A2,2 0 0,0 14,8A2,2 0 0,0 12,6M12,13C14.67,13 20,14.33 20,17V20H4V17C4,14.33 9.33,13 12,13M12,14.9C9.03,14.9 5.9,16.36 5.9,17V18.1H18.1V17C18.1,16.36 14.97,14.9 12,14.9Z" />
</svg>
           <span class="rounded"> Поручить</span>
        </span>
        <span class="mt-3 tags-custom">
 <svg style="width:24px;height:24px" viewBox="0 0 24 24">
    <path fill="currentColor" d="M14 15C14 16.11 13.11 17 12 17S10 16.11 10 15 10.9 13 12 13 14 13.9 14 15M6 20V10H18V13.09C18.33 13.04 18.66 13 19 13C19.34 13 19.67 13.04 20 13.09V10C20 8.9 19.11 8 18 8H17V6C17 3.24 14.76 1 12 1S7 3.24 7 6H9C9 4.34 10.34 3 12 3S15 4.34 15 6V8H6C4.89 8 4 8.9 4 10V20C4 21.1 4.89 22 6 22H13.81C13.46 21.39 13.22 20.72 13.09 20H6M15 18V20H23V18H15Z" />
</svg>
           <span class="rounded"> Доступ</span>
        </span>
        <span class="mt-3 tags-custom">
<svg style="width:24px;height:24px" viewBox="0 0 24 24">
    <path fill="currentColor" d="M7,12H9V14H7V12M21,6V20A2,2 0 0,1 19,22H5C3.89,22 3,21.1 3,20V6A2,2 0 0,1 5,4H6V2H8V4H16V2H18V4H19A2,2 0 0,1 21,6M5,8H19V6H5V8M19,20V10H5V20H19M15,14V12H17V14H15M11,14V12H13V14H11M7,16H9V18H7V16M15,18V16H17V18H15M11,18V16H13V18H11Z" />
</svg>
           <span class="rounded">Выбрать дату</span>
        </span>
        <span class="mt-3 tags-custom " v-for="(key, value) in selectedTask.tags" :key=value>
          <svg style="width:24px;height:24px" viewBox="0 0 24 24">
    <path fill="currentColor" d="M21.4 11.6L12.4 2.6C12 2.2 11.5 2 11 2H4C2.9 2 2 2.9 2 4V11C2 11.5 2.2 12 2.6 12.4L11.6 21.4C12 21.8 12.5 22 13 22C13.5 22 14 21.8 14.4 21.4L21.4 14.4C21.8 14 22 13.5 22 13C22 12.5 21.8 12 21.4 11.6M13 20L4 11V4H11L20 13M6.5 5C7.3 5 8 5.7 8 6.5S7.3 8 6.5 8 5 7.3 5 6.5 5.7 5 6.5 5M10.1 8.9L11.5 7.5L17 13L15.6 14.4L10.1 8.9M7.6 11.4L9 10L13 14L11.6 15.4L7.6 11.4Z" />
</svg>
           <span class="rounded custom-method"> {{ tags[key].name }}</span>
        </span>
      </div>
      <div class="mt-3 description-content">
        <div>{{ selectedTask.comment }}</div>
      </div>
      <div class="mt-3 list-files-custom" v-if="taskFiles.length">
        <!--<p class="text-center">Файлы</p>-->
        <div class="text-center"></div>
        <div class="mt-3 " v-for="(key, value) in taskFiles" :key=value>
           <div class="file-custom_attach"><svg style="width:35px;height:35px" viewBox="0 0 24 24">
             <path fill="currentColor" d="M11,4H13V16L18.5,10.5L19.92,11.92L12,19.84L4.08,11.92L5.5,10.5L11,16V4Z" />
           </svg><a v-bind:href="key.file_name">{{ key.file_name }}</a></div>
        </div>
      </div>

      <div class="mt-3 chat-custom" v-if="taskMessages.length">
        <p class="text-center date-messages-chat">{{ selectedTask.date_create }}</p>
        <div class="mt-3" v-for="(key, value) in taskMessages" :key=value>
           <div class="flex">
          <!--   <img :src="employees[key.uid_creator].fotolink" class="mr-1 rounded border-solid border-2 border-sky-500" width="30" height="30">-->
             <div>
               <p v-if="key.uid_creator==key.uid_creator">{{employees[key.uid_creator].name}}</p>
             </div>
           </div>

           <div class="mt-1 msg-custom-chat" v-if="key.uid_creator!==key.uid_creator" style="background-color:#FCEAEA;">{{ key.msg }}
           <div class="time-chat">{{ key.date_create }}</div>
           </div>
          <div class="mt-1 msg-custom-chat" v-else style="background-color:#FCEAEA;">{{ key.msg }}
            <div class="time-chat">{{ key.date_create  }}</div>
          </div>
        </div>
      </div>
      <!-- <ul>
        <li v-for="(item, index) in selectedTask.checklist" :key="item">
          {{ index.name }}
        </li>
      </ul> -->
      <template v-for="(menuGroup, index) in menu">
        <p
          v-if="typeof menuGroup === 'string'"
          :key="`a-${index}`"
          class="p-3 text-xs uppercase text-gray-400"
        >
          {{ menuGroup }}
        </p>
        <aside-menu-list
          v-else
          :key="`b-${index}`"
          :menu="menuGroup"
          @menu-click="menuClick"
        />
      </template>
    </div>
  </aside>
</template>
