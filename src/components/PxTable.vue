<template>
  <table>
    <thead>
      <tr class="bg-gray-100 border-b-2 border-gray-400">
        <th>
          <span>Comunidad</span>
        </th>
        <th>Municipio</th>
        <th>Departamento</th>
        <th>Cantidad</th>
        <th>Prioridad</th>
        <th>Estatus</th>
        <th></th>
        <td class="hidden sm:block"></td>
      </tr>
    </thead>
    <tbody>
      <tr
       v-for="comunidad in comunidades" :key="comunidad.id" clase="border-b border-gray-200 hover:bg-gray-100 hover:bg-orange-100">
        <td>{{ comunidad.nombre }}</td>
        <td>{{ comunidad.municipio }}</td>
        <td>{{ comunidad.departamento }}</td>
        <td>{{ comunidad.cantidad }}</td>
        <td>{{ comunidad.prioridad }}</td>
        <template v-if="comunidad.status == true">
            <td>
                <button class="bg-transparent hover:bg-red-500 text-red-700 font-semibold hover:text-white py-2 px-4 border border-red-500 hover:border-transparent rounded">
                 No Aplica
                </button>
            </td>
        </template>
        <template v-if="comunidad.status== false">
            <td><button class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded">
                 Aplica
                </button></td>
        </template>
        <td class="hidden sm:block"></td>

      </tr>
    </tbody>
  </table>
</template>
<script>

import gql from 'graphql-tag'

export default {
  name: "PxTable",
  apollo: {
      comunidades: {
          query:  gql`{
              getComunidades{
                  nombre
                  municipio
                  departamento
                  cantidad
                  prioridad
                  status
              }
          }`, update(data){
              return data.getComunidades
          }
      }
  },
  props: {
    assets: {
      type: Array,
      default: () => []
    }
  }
};
</script>

<style scoped>
.up::before {
  content: "👆";
}

.down::before {
  content: "👇";
}

td {
  padding: 20px 0px;
  font-size: 0.6rem;
  text-align: center;
}

th {
  padding: 5px;
  font-size: 0.6rem;
}

@media (min-width: 640px) {
  td,
  th {
    padding: 20px;
    font-size: 1rem;
  }

  th {
    padding: 12px;
  }
}
</style>
