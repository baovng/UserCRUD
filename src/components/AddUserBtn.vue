<template>
    <span>
        <button
         type="button"
         class="btn btn-primary"
         @click="this.addModal.toggle()"
        >
            Add a User
        </button>

        <div
            class="modal fade"
            ref="addUserDialog"
            id="addUserDialog"
            tabindex="-1"
            aria-labelledby="exampleModalLabel"
            aria-hidden="true"
        >
            <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Add a User</h5>
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
                    <label for="username-add" class="col-sm-2 col-form-label"
                        >Name</label
                    >
                    <div class="col-sm-10">
                        <input
                        type="text"
                        class="form-control"
                        v-model="name"
                        />
                    </div>
                    </div>
                    <div class="form-group row">
                    <label for="company-add" class="col-sm-2 col-form-label"
                        >Company</label
                    >
                    <div class="col-sm-10">
                        <input
                        type="text"
                        class="form-control"
                        v-model="company"
                        />
                    </div>
                    </div>
                    <div class="form-group row">
                    <label for="salary-add" class="col-sm-2 col-form-label"
                        >Salary</label
                    >
                    <div class="col-sm-10">
                        <input
                        type="text"
                        class="form-control"
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
                <button type="button" class="btn btn-primary" @click="handleClick()">
                    Add
                </button>
                </div>
            </div>
            </div>
        </div>
    </span>
</template>

<script>
export default {
    data: () => ({
        addModal: null,
        name: '',
        company: '',
        salary: ''
    }),
    mounted(){
        this.addModal = new bootstrap.Modal(this.$refs.addUserDialog)
    },
    methods: {
        handleClick(){
            if(!this.name.trim() || !this.company.trim() || !this.salary.trim()){
                alert('Fill all the fields')
                return
            }
            this.$emit('addUser', {
                name: this.name,
                company: this.company,
                salary: this.salary
            })

            this.name = ''
            this.company = ''
            this.salary = ''
            this.addModal.hide()
        }
    }
}
</script>