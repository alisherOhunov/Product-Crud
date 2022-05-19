// eslint-disable-next-line vue/multi-word-component-productNames
<template>
    <div>
        <h1 class="text-center">Product Crud</h1>
        <div class="my-2">
            <v-row >
                <v-dialog
                v-model="dialog"
                max-width="550px"
                >
                <template v-slot:activator="{ on, attrs }">
                    <v-btn
                    class="my-5"
                    color="primary"
                    dark
                    v-bind="attrs"
                    v-on="on"
                    >
                    Create
                    </v-btn>
                </template>
                <v-card>
                    <v-card-title>
                    <span class="text-h5">Create a new User</span>
                    </v-card-title>
                    <v-card-text>
                    <v-container>
                        <v-row>
                        <v-col
                            cols="12"
                        >
                            <v-text-field
                            class="productNameInput"
                            label="Product Name*"
                            v-model="productName"
                            outlined
                            required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                            class="serialNumberInput"
                            label="Product Serial Number*"
                            v-model="serialNumber"
                            outlined
                            required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-textarea
                            class="desctiptionInput"
                            label="Description*"
                            v-model="description"
                            outlined
                            type="text"
                            required
                            ></v-textarea>
                        </v-col>
                        </v-row>
                    </v-container>
                    </v-card-text>
                    <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                        class="cencel-btn"
                        @click="cencelAction"
                    >
                        Cencel
                    </v-btn>
                    <v-btn
                        v-if="!isEditing"
                        class="submit-btn"
                        @click="storeToList"
                    >
                        Save
                    </v-btn>
                     <v-btn
                        v-else-if="isEditing"
                        class="submit-btn"
                        @click="updateList()"
                    >
                        Update
                    </v-btn>
                    </v-card-actions>
                </v-card>
                </v-dialog>
            </v-row>
        </div>
        <template>
            <v-simple-table>
                <template v-slot:default>
                    <thead>
                        <tr>
                            <th class="text-left">
                                Id
                            </th>
                            <th class="text-left">
                                Product Name
                            </th>
                            <th class="text-left">
                                Product Serial Number
                            </th>
                            <th class="text-left">
                                Description
                            </th>
                            <th class="text-left">
                                Action
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr
                        v-for="item, index  in result"
                        :key="item.index"
                        >   
                            <td>{{index + 1}}</td>
                            <td>{{item[0]}}</td>
                            <td>{{item[1]}}</td>
                            <td>{{item[2] }}</td>
                            <td class="text-right">
                                <div class="d-flex justify-end">
                                    <v-btn
                                        class="edit-btn"
                                        depressed
                                        @click="editList(index, item[0], item[1], item[2])"
                                        >
                                            <v-icon left>
                                                mdi-pencil
                                            </v-icon>
                                        Edit
                                    </v-btn>
                                    <v-btn
                                        @click="removeFromList(index)"
                                        class="delete-btn mx-1"
                                        depressed
                                        color="error"
                                        >
                                        Delete
                                    </v-btn>
                                </div>
                            </td>
                        </tr>
                    </tbody>
                </template>
            </v-simple-table>
        </template>
    </div>
</template>
<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name:"Table",
    data () {
        return {
            dialog: false,
            isEditing: false,
            productName: "",
            serialNumber: null,
            description:"",
            selected: null,
            idNumber: null,
            gatheredList:[],
            result: [['Laptop', 343553535,'A laptop computer, sometimes called a notebook']]
        }
    },
    methods: {
    storeToList() {
        if(this.description && this.productName && this.serialNumber !== ""){
            this.gatheredList.push(this.productName)
            this.gatheredList.push(this.serialNumber)
            this.gatheredList.push(this.description)
            this.result.push(this.gatheredList)
            this.gatheredList = []
            this.productName = ''
            this.description = ''
            this.serialNumber = ''
            this.dialog = false
        }
        else{
            return
        }
    },

    removeFromList(index) {
        this.result.splice(index, 1)
    },

    updateList() {
       if(this.description && this.productName && this.serialNumber !== ""){
            this.result[this.idNumber].splice(this.selected, 1, this.productName, this.serialNumber, this.description)
            this.productName = ''
            this.serialNumber = ''
            this.description = ''
            this.isEditing = false
            this.dialog = false
       }
        else{
            return
        }
    },

    editList(index,productName, serialNumber, description) {
        this.idNumber = index
        this.dialog = true
        this.isEditing = true
        this.productName = productName
        this.serialNumber = serialNumber
        this.description = description
        this.selectedIndex = index
    },
    cencelAction(){
        this.dialog = false,
        this.isEditing = false,
        this.productName = "",
        this.serialNumber = "",
        this.description = ""
    }
}
}
</script>