<template>
    <section  class="flex">
        <div class="mx-auto mt-10 ">
            <table  class="text-center">
                <thead >
                    <th class="p-3 px-3" >Emp_ID</th>
                    <th class="p-3 px-3">Emp_Name</th>
                    <th class="p-3 px-3">Emp_Phone</th>
                    <th class="p-3 px-3">Emp_description</th>
                </thead>
                <tr v-for="employee in employees" :key="employee.id" class="p-3">
                    <td>{{ employee.id }}</td>
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.phone }}</td>
                    <td>{{ employee.designation }}</td>
                    <td>
                        <button @click="editEmp(employee)" class="mx-4 bg-green-600 px-4 border border-black">Edit</button>
                        <button @click="deleteEmp(employee)" class="mx-4  px-4 border border-black">delete</button>
                    </td>
                </tr>  
            </table>
            <button @click="dialog=true" class="mt-5 border border-black px-7 rounded-1xl">Add +</button>
        </div>
        <!---------------Dialog--------------------->
        <dialog :open="dialog" class="border border-black mt-10 p-10">
            <div class=" ">
               <label class=" font-bold">Emp_ID</label>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;
               <input type="text" v-model="id"  placeholder="id"/><br><br>
               <label class=" font-bold">Emp_Name</label>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;
               <input type="text" v-model="name" placeholder="Name"/><br><br>
               <label class=" font-bold">Emp_Phone</label>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;
               <input type="text"  v-model="phone"  placeholder="Phone"/><br><br>
               <label class=" font-bold">Emp_Description</label>&nbsp;:&nbsp;&nbsp;
               <input type="text"  v-model="designation"  placeholder="designation"/><br><br>
               <button v-if="!editing"  @click="addEmp"  class="border border-black px-5 bg-green-500">Save</button>
               <button v-else @click="updateEmp"  class="border border-black px-5 bg-blue-500">Update</button>
               <button @click="close" class="border border-black px-5 bg-red-500  md:ml-10">Cancel</button>
               
            </div>
        </dialog>
    </section>
</template>
<!---------------script------------------------------>
<script>
export default{
    name:'employee-information',
    data(){
        return{
            employees:[],
            id:'',
            name:'',
            phone:'',
            designation:'',
            dialog:false,
            editing:false,
            selectEmployee:{}
        };
    },
    methods:{
        addEmp(){
            console.log(this.id)
            this.employees.push(
                {
                    id:this.id,
                    name:this.name,
                    phone:this.phone,
                    designation:this.designation
                }
            )
            this.close()
        },
        deleteEmp(employee){
            let index=this.employees.indexOf(employee)
            this.employees.splice(index,1)
        },

        editEmp(emp){
            this.id=emp.id
            this.name=emp.name
            this.phone=emp.phone
            this.designation=emp.designation
            this.dialog=true
            this.editing=true
            this.selectEmployee=emp
        },

        updateEmp(){
            let index= this.employees.indexOf(this.selectEmployee)
            this.employees.splice(index,1)
            this.employees.push(
                {
                    id:this.id,
                    name:this.name,
                    phone:this.phone,
                    designation:this.designation
                }
            )
            this.close()
        },

        close(){
            this.id=''
            this.name=''
            this.phone=''
            this.designation=''
            this.editing=false
            this.dialog=false
        }
    }
}
</script>


<!--------------------style---------------------------------->
<style scoped>
table,tr,td,th{
    border:1px solid black;
}
.color{
    color:green;
}

</style>