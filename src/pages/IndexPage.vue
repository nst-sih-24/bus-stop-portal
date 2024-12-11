<template>
  <q-page class="q-pa-md">
    <pre>{{ vehicles }}</pre>

    <q-table :rows="buses" :columns="columns" row-key="name" flat bordered title="Upcoming Buses">
    </q-table>
  </q-page>
</template>

<script setup>
// capacity of next bus
// available capacity of next bus
// occupied capacity of next bus
// how many seats will be available in next bus when people drop off at this stop
// next bus time for same route
// all buses from different routes cronologically

import { onMounted, ref } from 'vue'
import { supabase } from 'boot/supabase'

const columns = [
  { name: 'route', label: 'Route', align: 'center', field: 'route' },
  { name: 'time', label: 'Time', align: 'center', field: 'time' },
  { name: 'busNumber', label: 'Bus Number', align: 'center', field: 'busNumber' },
  { name: 'available', label: 'Available', align: 'center', field: 'available' },
  { name: 'occupied', label: 'Occupied', align: 'center', field: 'occupied' },
  { name: 'dropOff', label: 'Drop Off', align: 'center', field: 'dropOff' },
  { name: 'capacity', label: 'Capacity', align: 'center', field: 'capacity' },
  { name: 'nextBusTime', label: 'Next Bus', align: 'center', field: 'nextBusTime' },
]

const buses = ref([
  {
    route: 'A',
    capacity: 50,
    available: 20,
    occupied: 30,
    dropOff: 5,
    time: '10:00',
    busNumber: 'DL 01 ER 0001',
    nextBusTime: '10:30',
  },
  {
    route: 'B',
    capacity: 50,
    available: 20,
    occupied: 30,
    dropOff: 5,
    time: '10:05',
    busNumber: 'DL 01 ER 0002',
    nextBusTime: '10:35',
  },
  {
    route: 'C',
    capacity: 50,
    available: 20,
    occupied: 30,
    dropOff: 5,
    time: '10:10',
    busNumber: 'DL 01 ER 0002',
    nextBusTime: '10:40',
  },
])

const vehicles = ref([])

const fetchVehicles = async () => {
  const { data, error } = await supabase.from('vehicles').select('*')
  if (error) {
    console.error(error)
  } else {
    vehicles.value = data
  }
}

onMounted(() => {
  fetchVehicles()
})

</script>
