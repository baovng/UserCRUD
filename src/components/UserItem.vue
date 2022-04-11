<template>
    <tr>
        <td>{{user.index}}</td>
        <td>{{user.name}}</td>
        <td>{{user.isActive}}</td>
        <td>{{user.salary}}</td>
        <td>{{user.company}}</td>
        <td>
            <button type="button" class="btn btn-info" @click="editModal.show()">Edit</button>
            <button type="button" class="btn btn-danger" @click="$emit('delete')">Delete</button>

            <div
                class="modal fade"
                ref="editUserDialog"
                id="editUserDialog"
                tabindex="-1"
                aria-labelledby="exampleModalLabel"
                aria-hidden="true"
            >
                <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">Edit a User</h5>
                    <button
                        type="button"
                        class="btn-close"
                        data-bs-dismiss="modal"
                        aria-label="Close"
                    ></button>
                    </div>
                    <div class="modal-body">
                    <form>
                        <div class="form-group row">
                        <label for="username-edit" class="col-sm-2 col-form-label"
                            >Name</label
                        >
                        <div class="col-sm-10">
                            <input
                            type="text"
                            readonly
                            class="form-control-plaintext"
                            id="username-edit"
                            :value="user.name"
                            />
                        </div>
                        </div>
                        <div class="form-group row">
                        <label for="salary-edit" class="col-sm-2 col-form-label"
                            >Salary</label
                        >
                        <div class="col-sm-10">
                            <input
                            type="text"
                            class="form-control"
                            id="salary-edit"
                            v-model="salary"
                            />
                        </div>
                        </div>
                    </form>
                    </div>
                    <div class="modal-footer">
                    <button
                        type="button"
                        class="btn btn-secondary"
                        data-bs-dismiss="modal"
                    >
                        Close
                    </button>
                    <button
                        type="button"
                        class="btn btn-primary"
                        @click="handleClick"
                    >
                        Save changes
                    </button>
                    </div>
                </div>
                </div>
            </div>
        </td>
    </tr>

    
</template>

<script>
export default {
    props: ['user'],
    data: () => ({
        editModal: null,
        salary: 0
    }),
    mounted(){
        this.editModal = new bootstrap.Modal(this.$refs.editUserDialog)
        this.salary = this.user.salary
    },
    methods: {
        handleClick(){
            if(!this.salary.trim()){
                alert('Salary is required')
                return
            }
            this.$emit('update', this.salary)

            this.editModal.hide()
        }
    }
}
</script>