<template>
    <div>
        <Select v-model="model1" style="width:200px" dropdownCssClass="aims">
            <Option v-for="item in cityList" :value="item.value" :key="item.value">{{ item.label }}</Option>
        </Select>

        <Select v-model="model2" multiple style="width:200px">
            <Option v-for="item in cityList" :value="item.value" :key="item.value">{{ item.name }}</Option>
        </Select>

        <Select v-model="model3" style="width:200px">
            <Option v-for="item in cityList" :value="item" :key="item.value">{{ item.name }}</Option>
        </Select>

        <button @click="add">
            add
        </button>
        <button @click="show">
            show
        </button>

        <div v-if="added">
            <Select v-model="model3"
                    filterable 
                    remote 
                    :remote-method="remoteMethod1"
                    textField="name"
                    style="width:200px">
                <Option v-for="item in options3" :value="item" :key="item.label">{{ item.name }}</Option>
            </Select>
        </div>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                cityList: [
                    {
                        value: 'New York',
                        name: 'New York'
                    },
                    {
                        value: 'London',
                        name: 'London'
                    },
                    {
                        value: 'Sydney',
                        name: 'Sydney'
                    },
                    {
                        value: 'Ottawa',
                        name: 'Ottawa'
                    },
                    {
                        value: 'Paris',
                        name: 'Paris'
                    },
                    {
                        value: 'Canberra',
                        name: 'Canberra'
                    }
                ],
                model1: '',
                model2: [],
                model3: {
                        value: 'Canberra',
                        name: 'Canberra'
                    },
                added: false,
                loading3: false,
                options3: [],
            }
        },
        methods: {
            add() {
                this.model3 = this.cityList[0];
            },
            add2() {
                this.model3 = this.cityList[2];
            },
            show() {
                this.added = !this.added;
            },
            remoteMethod1 (query) {
                if (query !== '') {
                    this.loading3 = true;
                    setTimeout(() => {
                        this.loading3 = false;
                        this.options3 = this.cityList.filter(item => item.name.toLowerCase().indexOf(query.toLowerCase()) > -1);
                    }, 200);
                } else {
                    this.options3 = [];
                }
            },
        }
    }
</script>
