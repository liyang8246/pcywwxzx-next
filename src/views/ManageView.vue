<script setup>
import TableItem from '@/components/TableItem.vue';
import { ref, onMounted } from 'vue';
import axios from 'axios';
axios.defaults.baseURL = import.meta.env.VITE_BACKEND_URL;

const passwd = ref('');
const issueList = ref([]);
const getIssueList = () => {
  axios
    .get('/api/issue?passwd=' + passwd.value)
    .then((res) => {
      issueList.value = res.data.slice(0, 32);
    })
    .catch((error) => {
      console.error(error);
    });
};
const toggleIssue = (issueId) => {
  axios
    .post(`/api/issue?passwd=${passwd.value}&id=${issueId}`)
    .then((res) => {
      getIssueList();
    })
    .catch((error) => {
      console.error(error);
    });
};
const deleteIssue = (issueId) => {
  axios
    .delete(`/api/issue?passwd=${passwd.value}&id=${issueId}`)
    .then((res) => {
      getIssueList();
    })
    .catch((error) => {
      console.error(error);
    });
};
</script>

<template>
  <div class="min-h-full flex flex-col items-center justify-center">
    <div class="flex justify-center items-center" v-show="!issueList.length">
      <div class="join max-w-sm">
        <input type="password" class="input join-item" v-model="passwd" placeholder="PassWord" />
        <button @click="getIssueList()" class="btn btn-outline btn-secondary join-item">LOGIN</button>
      </div>
    </div>
    <div class="flex justify-center items-center" v-show="issueList.length">
      <table class="table table-sm sm:table">
        <thead>
          <tr>
            <th>姓名</th>
            <th class="hidden md:table-cell">班级</th>
            <th class="hidden xl:table-cell">学号</th>
            <th class="hidden lg:table-cell">电话</th>
            <th>日期</th>
            <th>状态</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <TableItem
            @toggle-issue="toggleIssue(issue.id)"
            @delete-issue="deleteIssue(issue.id)"
            v-for="issue in issueList"
            :issue="issue"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>
