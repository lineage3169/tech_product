<template>
    <div>
        <b-button variant="success" v-b-modal.modal-1>新增商品</b-button>
        <b-modal id="modal-1" title="新增商品" @ok="addProduct()">
            <form ref="form">
            <b-form-group
                label="名稱"
                label-for="name-input">
                <b-form-input
                id="name-input"
                v-model="addForm.name"/>
            </b-form-group>
            <b-form-group
                label="尺寸"
                label-for="size-input" >
                <b-form-select id="size-input"
                                v-model="addForm.size" 
                                :options="sizeList"/>
            </b-form-group>
            <b-form-group
                label="價格"
                label-for="price-input" >
                <b-form-input
                id="price-input"
                type="number"
                v-model="addForm.price" />
            </b-form-group>
            <b-form-group
                label="數量"
                label-for="amount-input" >
                <b-form-input
                id="amount-input"
                type="number"
                v-model="addForm.amount" />
            </b-form-group>
            </form>
        </b-modal>
    </div>
</template>
<script>
export default {
    name: 'addProduct',
    props: ['propsData'],
    data() {
        return {
            addForm: {
                id: null,
                name: '',
                size: 'M',
                price: 0,
                amount: 0
            },
            sizeList: [
                {
                    value: 'XS',
                    text: 'XS'
                },
                {
                    value: 'S',
                    text: 'S'
                },
                {
                    value: 'M',
                    text: 'M'
                },
                {
                    value: 'L',
                    text: 'L'
                },
                {
                    value: 'XL',
                    text: 'XL'
                },
            ]
        }
    },
    methods: {
        addProduct() {
            // 找到 this.product 最後一筆ID
            const idList = this.propsData.map(item => {return item.id})
            idList.sort(function(a, b) {
                return b - a;
            });
            const lastId = idList[0]
            // 然後 +1 當作新商品的id
            this.addForm.id = lastId + 1
            // deep copy
            const obj = JSON.parse(JSON.stringify(this.addForm))
            
            // 什麼是傳值 什麼是傳址
            // 只要是Object都是記憶體位置
            // emit 子傳父
            this.$emit('add',obj)
        }
    },
}
</script>