<script setup>
import { ref } from 'vue';

const group = ref([]);
const newMember = ref('');

const emit = defineEmits(['groupCreated']);

function addMember() {
  const trimmed = newMember.value.trim();
  if (
    trimmed &&
    !group.value.find(person => person.name.toLowerCase() === trimmed.toLowerCase())
  ) {
    group.value.push({
      name: trimmed,
      currentContribution: 0,
      owes: 0
    });
    newMember.value = '';
  }
}

function removeMember(index) {
  group.value.splice(index, 1);
}

function createGroup() {
  if (group.value.length > 0) {
    emit('groupCreated', group.value);
  } else {
    alert('Add at least one member!');
  }
}
</script>

<template>
  <div class="container mt-5">
    <div class="bg-primary text-white text-center py-3 rounded-top shadow-sm">
      <h1 class="mb-0">Let’s Do Dutch</h1>
      <p class="mb-0 small">Create your group and split smart</p>
    </div>

    <div class="card shadow border-0 rounded-bottom">
      <div class="card-body bg-light">
        <h2 class="h4 mb-4 text-primary">Create Group</h2>

        <div class="mb-3">
          <label class="form-label">Enter Member Name</label>
          <div class="d-flex align-items-start gap-2">
            <input
              v-model="newMember"
              type="text"
              class="form-control"
              placeholder="Enter name"
              @keyup.enter="addMember"
            />
            <button
              @click="addMember"
              class="btn btn-success"
              style="min-width: 100px;"
            >
              Add
            </button>
          </div>
        </div>

        <h5 class="mb-3 text-secondary">Group Members</h5>
        <ul class="list-group mb-4">
          <li
            v-for="(person, index) in group"
            :key="index"
            class="list-group-item d-flex justify-content-between align-items-center"
          >
            {{ person.name }}
            <button
              @click="removeMember(index)"
              class="btn btn-outline-danger btn-sm"
              title="Remove person"
            >
              Remove
            </button>
          </li>
        </ul>

        <button
          @click="createGroup"
          class="btn btn-primary w-100"
        >
          Create Group
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
