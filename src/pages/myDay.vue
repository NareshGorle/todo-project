<template>
    <q-page class="bg-grey-3 column">
        <div class="row q-pa-sm bg-primary">
            <q-input
              v-model="newTask"
              class="col"
              square
              filled
              bg-color="white" 
              bottom-slot
              placeholder="Add task"
              @keyup.enter="addTask"
              dense>
        <template v-slot:append>
          <q-btn 
           @click="addTask"
           round
           dense
           flat
           icon="add" />
        </template>
      </q-input>
        </div>
        <q-list 
        class="bg-white"
        separator
        bordered
        >
       <q-item 
       v-for="(task,index) in tasks"
         :key="task.title"
         @click="task.done=!task.done"
        :class="{'done':task.done}"
        v-ripple>

        <q-item-section avatar>
          <q-checkbox
           clickable
           v-model="task.done"
           color="primary" 
           /> 
        </q-item-section> 

        <q-item-section>

          <q-item-label v-if="!task.isEditing">
            {{ task.title }}
          </q-item-label>

          <q-input
            v-else
            v-model="task.title"
            dense
            autofocus
            @blur="saveEdit(index)"
            @keyup.enter="saveEdit(index)"
          />
        </q-item-section>


        <q-item-section side top>
        <q-item-label caption>{{ todaysDate }}  </q-item-label>
        </q-item-section>

        <q-item-section side>
          <q-btn
            v-if="!task.isEditing"
            @click="editTask(index)"
            round
            dense
            flat
            color="primary"
            icon="edit"
          />
          <q-btn
            v-if="task.done"
            @click="deleteTask(index)"
            push
            round
            color="primary"
            icon="delete"
          />
        </q-item-section>
        
      </q-item>
     
    </q-list>
    <div
        v-if="!tasks.length"
        class="no-task absolute-center">
        <q-icon
        name="check"
        size="100px"
        color="primary"/>
        <div class="text-h5 text-primary text-center"> No tasks</div>
    </div>
        
    </q-page>
</template>

<script>
import { useQuasar,date } from 'quasar'
import { ref,computed,onMounted,watch} from 'vue'
    export default {
        setup(){
            const newTask = ref('')
            const tasks = ref({})
          
           
            const $q = useQuasar()
            const addTask=()=>{
                if (newTask.value.trim() !== "") {
                 tasks.value.push({ title: newTask.value , done:false});
                  newTask.value = "";
                 
                 }
        }
                const deleteTask =(index)=>{
                   $q.dialog({
                        title: 'Confirm',
                        message: 'Are you sure ?',
                        cancel: true,
                        persistent: true
                    }).onOk(() => {
                        tasks.value.splice(index,1) 
                        $q.notify('Task deleted')
                       
                    })
              
            }

           const todaysDate = computed(()=>{
             let timeStamp = Date.now()
           return date. formattedString = date.formatDate(timeStamp, 'D MMM')
              })


              watch(tasks, (newTasks) => {
                    window.localStorage.setItem("tasks", JSON.stringify(newTasks));
                    }, { deep: true });


              onMounted(() => {
                const saveTask = window.localStorage.getItem("tasks");
                 if (saveTask) {
                       tasks.value = JSON.parse(saveTask);
                           }
                  });
        

             const editTask = (index) => {
                tasks.value[index].isEditing = true;
                  };

               const saveEdit = (index) => {
                 tasks.value[index].isEditing = false;
                  };

            return{
               tasks,
               newTask,
               addTask,
               deleteTask,
               todaysDate,
               editTask,
               saveEdit,
               
            }
        }
    }
</script>

<style lang="scss">
.done{ 
      .q-item__label{
            text-decoration: line-through;
            color:inherit;
        }
       
    }
.done{
    .q-item__label--caption{
            text-decoration: none;
            color:inherit;
        }
}

      
    


.no-tasks{
    opacity: 0.5;
}




</style>