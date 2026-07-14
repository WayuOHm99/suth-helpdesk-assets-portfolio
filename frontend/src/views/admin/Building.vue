<script setup>
import { ref, onMounted } from "vue"
import api from "../../services/api"

const buildings = ref([])
const newBuilding = ref("")

const editingId = ref(null)
const editName = ref("")

// โหลดข้อมูล
async function load() {
  try {
    const res = await api.get("/buildings")
    buildings.value = res.data
  } catch (err) {
    console.error(err)
    alert("โหลดข้อมูลไม่สำเร็จ")
  }
}

// เพิ่ม
async function addBuilding() {
  if (!newBuilding.value.trim()) {
    alert("กรุณากรอกชื่ออาคาร")
    return
  }

  try {
    await api.post("/buildings", {
      name: newBuilding.value,
    })

    newBuilding.value = ""
    load()
  } catch (err) {
    console.error(err)
    alert("เพิ่มข้อมูลไม่สำเร็จ")
  }
}

// เริ่มแก้ไข
function editBuilding(building) {
  editingId.value = building.id
  editName.value = building.name
}

// บันทึก
async function saveBuilding(id) {
  if (!editName.value.trim()) {
    alert("กรุณากรอกชื่ออาคาร")
    return
  }

  try {
    await api.put(`/buildings/${id}`, {
      name: editName.value,
    })

    editingId.value = null
    editName.value = ""

    load()
  } catch (err) {
    console.error(err)
    alert("แก้ไขข้อมูลไม่สำเร็จ")
  }
}

// ลบ
async function deleteBuilding(id) {
  if (!confirm("ต้องการลบอาคารนี้ใช่หรือไม่?")) return

  try {
    await api.delete(`/buildings/${id}`)
    load()
  } catch (err) {
    console.error(err)
    alert("ลบข้อมูลไม่สำเร็จ")
  }
}

onMounted(load)
</script>

<template>
  <div class="p-6">
    <h1 class="text-2xl font-bold mb-4">
      Building Management
    </h1>

    <!-- เพิ่ม -->
    <div class="flex gap-2 mb-6">
      <input
        v-model="newBuilding"
        type="text"
        placeholder="Building Name"
        class="border rounded px-3 py-2"
      />

      <button
        @click="addBuilding"
        class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600"
      >
        Add
      </button>
    </div>

    <!-- ตาราง -->
    <table class="w-full border-collapse border">

      <thead>
        <tr>
          <th class="border p-2">ID</th>
          <th class="border p-2">Building</th>
          <th class="border p-2">Action</th>
        </tr>
      </thead>

      <tbody>

        <tr
          v-for="b in buildings"
          :key="b.id"
        >

          <td class="border p-2">
            {{ b.id }}
          </td>

          <td class="border p-2">

            <span v-if="editingId !== b.id">
              {{ b.name }}
            </span>

            <input
              v-else
              v-model="editName"
              class="border rounded px-2 py-1 w-full"
            />

          </td>

          <td class="border p-2 space-x-2">

            <template v-if="editingId !== b.id">

              <button
                @click="editBuilding(b)"
                class="bg-yellow-500 text-white px-3 py-1 rounded"
              >
                Edit
              </button>

              <button
                @click="deleteBuilding(b.id)"
                class="bg-red-600 text-white px-3 py-1 rounded"
              >
                Delete
              </button>

            </template>

            <button
              v-else
              @click="saveBuilding(b.id)"
              class="bg-green-600 text-white px-3 py-1 rounded"
            >
              Save
            </button>

          </td>

        </tr>

      </tbody>

    </table>

  </div>
</template>