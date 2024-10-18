<script setup lang="ts">
// 1. Manipulação de usuário e grupo
// 2. Manipulação de Permissões
// 3. Manipulação de Arquivos e Diretórios
import { ref, computed } from 'vue'

const user = ref('')
const group = ref('')

const resource = ref('')
const folder = ref(false)
const uPermissions = ref([])
const gPermissions = ref([])
const oPermissions = ref([])

const userName = computed(() => {
  return user.value || '<user name>'
})

const groupName = computed(() => {
  return group.value || '<group name>'
})

const folderLabel = computed(() => {
  return folder.value ? ' -R' : ''
})

const resourceName = computed(() => {
  return resource.value || '<resource name>'
})

const userPermissions = computed(() => {
  let total = 0
  uPermissions.value.forEach(value => {
    total += value
  })
  return total
})

const groupPermissions = computed(() => {
  let total = 0
  gPermissions.value.forEach(value => {
    total += value
  })
  return total
})

const otherPermissions = computed(() => {
  let total = 0
  oPermissions.value.forEach(value => {
    total += value
  })
  return total
})
</script>

<template>
  <div class="about">
    <div class="flex flex-column gap">
      <h1>Command generator</h1>
      <div>
        <input v-model="user" type="text" placeholder="User Name" />
        <input v-model="group" type="text" placeholder="Group Name" />
        <input v-model="resource" type="text" placeholder="Resource Name" />
        <label for="folder">Folder?</label>
        <input
          v-model="folder"
          id="folder"
          type="checkbox"
          placeholder="Resource Name"
          :value="-R"
        />
      </div>
      <div>
        <div>
          Users:
          <label for="readPermission1">Read: </label>
          <input
            v-model="uPermissions"
            type="checkbox"
            name="permission"
            id="readPermission1"
            :value="4"
          />

          <label for="writePermission1">Write: </label>
          <input
            v-model="uPermissions"
            type="checkbox"
            name="permission"
            id="writePermission1"
            :value="2"
          />

          <label for="execPermission1">Exec: </label>
          <input
            v-model="uPermissions"
            type="checkbox"
            name="permission"
            id="execPermission1"
            :value="1"
          />
        </div>

        <div>
          Groups:
          <label for="readPermission2">Read: </label>
          <input
            v-model="gPermissions"
            type="checkbox"
            name="permission"
            id="readPermission2"
            :value="4"
          />

          <label for="writePermission2">Write: </label>
          <input
            v-model="gPermissions"
            type="checkbox"
            name="permission"
            id="writePermission2"
            :value="2"
          />

          <label for="execPermission2">Exec: </label>
          <input
            v-model="gPermissions"
            type="checkbox"
            name="permission"
            id="execPermission2"
            :value="1"
          />
        </div>

        <div>
          Others:
          <label for="readPermission3">Read: </label>
          <input
            v-model="oPermissions"
            type="checkbox"
            name="permission"
            id="readPermission3"
            :value="4"
          />

          <label for="writePermission3">Write: </label>
          <input
            v-model="oPermissions"
            type="checkbox"
            name="permission"
            id="writePermission3"
            :value="2"
          />

          <label for="execPermission3">Exec: </label>
          <input
            v-model="oPermissions"
            type="checkbox"
            name="permission"
            id="execPermission3"
            :value="1"
          />
        </div>
      </div>

      <h1>Commands</h1>

      <div class="flex-column">
        <h2>Users</h2>
        <pre>
          sudo adduser {{ userName }}
          sudo chown{{ folderLabel }} {{ userName }} {{ resourceName }}
        </pre>
      </div>

      <div class="flex-column">
        <h2>Users and Groups</h2>
        <pre>
          sudo addgroup {{ userName }} {{ groupName }}
          sudo chown{{ folderLabel }} {{ userName }}:{{ groupName }} {{
            resourceName
          }}
        </pre>
      </div>

      <div class="flex-column">
        <h2>Groups</h2>
        <pre>
          sudo addgroup {{ groupName }}
          sudo chown{{ folderLabel }} {{ groupName }} {{ resourceName }}
          sudo chmod{{ folderLabel }} {{ userPermissions }}{{ groupPermissions
          }}{{ otherPermissions }} {{ resourceName }}
        </pre>
      </div>
    </div>
  </div>
</template>

<style>
.flex {
  display: flex;
}

.flex-column {
  flex-direction: column;
}

.flex-row {
  flex-direction: row;
}

.gap {
  gap: 10px;
}

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
