<template>
  <main>
    <el-form ref="attachForm" :model="products" label-position="top">
      <div class="buy_product">
        <el-form-item class="buy__product_item">
          <div class="product" @click="save_product('cola15'), buy_all()">
            <el-icon v-if="!products.cola15" class="el_icon"><Sell /></el-icon>
            <el-icon v-if="products.cola15" class="el_icon"><Plus /></el-icon>
            <el-badge :value="products.cola15">
              <img width="120" src="@/img/cola.png" alt="cola image" />
            </el-badge>
          </div>
          <el-text>
            Coca-cola 1.5L <br />
            <b> 12 000 so'm</b>
          </el-text>
        </el-form-item>

        <el-form-item class="buy__product_item">
          <div class="product" @click="save_product('cola1'), buy_all()">
            <el-icon v-if="!products.cola1" class="el_icon"><Sell /></el-icon>
            <el-icon v-if="products.cola1" class="el_icon"><Plus /></el-icon>
            <el-badge :value="products.cola1">
              <img width="120" src="@/img/coca-cola-1.png" alt="coca-cola-1 image" />
            </el-badge>
          </div>
          <el-text>
            Coca-cola 1L <br />
            <b> 9 000 so'm</b>
          </el-text>
        </el-form-item>

        <el-form-item class="buy__product_item">
          <div class="product" @click="save_product('cola05'), buy_all()">
            <el-icon v-if="!products.cola05" class="el_icon"><Sell /></el-icon>
            <el-icon v-if="products.cola05" class="el_icon"><Plus /></el-icon>
            <el-badge :value="products.cola05">
              <img width="120" src="@/img/yarim_cola.png" alt="yarim_cola image" />
            </el-badge>
          </div>
          <el-text>
            Coca-cola 0,5L <br />
            <b> 7 000 so'm</b>
          </el-text>
        </el-form-item>

        <el-form-item class="buy__product_item">
          <div class="product" @click="save_product('banana'), buy_all()">
            <el-icon v-if="!products.banana" class="el_icon"><Sell /></el-icon>
            <el-icon v-if="products.banana" class="el_icon"><Plus /></el-icon>
            <el-badge :value="products.banana">
              <img width="120" src="@/img/banana.png" alt="banana image" />
            </el-badge>
          </div>
          <el-text>
            Banan 1 kg <br />
            <b> 21 000 so'm</b>
          </el-text>
        </el-form-item>

        <el-form-item class="buy__product_item">
          <div class="product" @click="save_product('apple'), buy_all()">
            <el-icon v-if="!products.apple" class="el_icon"><Sell /></el-icon>
            <el-icon v-if="products.apple" class="el_icon"><Plus /></el-icon>
            <el-badge :value="products.apple">
              <img width="120" src="@/img/apples.png" alt="apples image" />
            </el-badge>
          </div>
          <el-text>
            Qizil olma 1 kg <br />
            <b> 23 000 so'm</b>
          </el-text>
        </el-form-item>

        <el-form-item class="buy__product_item">
          <div class="product" @click="save_product('juice'), buy_all()">
            <el-icon v-if="!products.juice" class="el_icon"><Sell /></el-icon>
            <el-icon v-if="products.juice" class="el_icon"><Plus /></el-icon>
            <el-badge :value="products.juice">
              <img width="120" src="@/img/juice.png" alt="juice image" />
            </el-badge>
          </div>
          <el-text>
            Dena Behili sok <br />
            <b> 13 000 so'm</b>
          </el-text>
        </el-form-item>
      </div>

      <div class="aside_" v-if="all">
        <div class="aside_big_item">
          <div class="aside_item" v-if="products.cola15">
            <img width="120" src="@/img/cola.png" alt="1L cola image" />
            <el-input-number controls-position="right" @change="buy_all" v-model="products.cola15" :min="0" :max="50" />
            <p>Cola 1.5L </p>
          </div>
          
          <div class="aside_item" v-if="products.cola1">
            <img width="120" src="@/img/coca-cola-1.png" alt="1L cola image" />
            <el-input-number controls-position="right" @change="buy_all" v-model="products.cola1" :min="0" :max="50" />
            <p>Cola 1L </p>
          </div>

          <div class="aside_item" v-if="products.cola05">
            <img width="120" src="@/img/yarim_cola.png" alt="0.5L cola image" />
            <el-input-number controls-position="right" @change="buy_all" v-model="products.cola05" :min="0" :max="50" />
            <p>Cola 0.5L </p>
          </div>

          <div class="aside_item" v-if="products.banana">
            <img width="120" src="@/img/banana.png" alt="banana image" />
            <el-input-number controls-position="right" @change="buy_all" v-model="products.banana" :min="0" :max="50" />
            <p>Banan</p>
          </div>

          <div class="aside_item" v-if="products.apple">
            <img width="120" src="@/img/apples.png" alt="apple image" />
            <el-input-number controls-position="right" @change="buy_all" v-model="products.apple" :min="0" :max="50" />
            <p>Banan</p>
          </div>

          <div class="aside_item" v-if="products.juice">
            <img width="120" src="@/img/juice.png" alt="juice image" />
            <el-input-number controls-position="right" @change="buy_all" v-model="products.juice" :min="0" :max="50" />
            <p>Dena behili sok</p>
          </div>
        </div>

        <div class="d-flex">
          <p><el-text tag="b">Jami:</el-text> {{ all }} so'm</p>
          <el-button plain type="success" @click="dialogVisible = true">
            Chek chiqarish
          </el-button>

          <el-dialog
            v-model="dialogVisible"
            title="Siz xarid qilgan mahsulotlar"
            width="550"
            :before-close="handleClose"
          >
            <template #footer>
              <div class="dialog-footer">
                <div>
                  <el-table :data="tableData" style="width: 100%">
                    <el-table-column v-if="products.cola05" prop="cola05" label="Coca Cola 0.5L" max-width="180" />
                    <el-table-column v-if="products.cola1" prop="cola1" label="Coca Cola 1L" max-width="180" />
                    <el-table-column v-if="products.cola15" prop="cola15" label="Coca Cola 1.5L" />
                    <el-table-column v-if="products.banana" prop="banana" label="Banan" max-width="180" />
                    <el-table-column v-if="products.apple" prop="apple" label="Olma" maxwidth="180" />
                    <el-table-column v-if="products.juice" prop="juice" label="Sharbat" max-width="180"/>
                  </el-table><br>
                  <p><el-text tag="b">Jami:</el-text> {{all}} so'm</p>
                  
                </div> <br>
                <el-button @click="dialogVisible = false">Yopish</el-button>
                <el-button type="primary" @click="dialogVisible = false">
                  Chekni chiqarish
                </el-button>
              </div>
            </template>
          </el-dialog>
        </div>
      </div><br>
    </el-form>
  </main>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const products = ref({
  cola05: 0,
  cola1: 0,
  cola15: 0,
  banana: 0,
  apple: 0,
  juice: 0
})
const all = ref()

const tableData = ref([])

const save_product = (product) => {
  if (product == 'cola05') {
    products.value.cola05++
  } else if (product == 'cola1') {
    products.value.cola1++
  } else if (product == 'cola15') {
    products.value.cola15++
  } else if (product == 'banana') {
    products.value.banana++
  } else if (product == 'apple') {
    products.value.apple++
  } else if (product == 'juice') {
    products.value.juice++
  }
  tableData.value = [
  {
    cola05: products.value.cola05 + " dona",
    cola1: products.value.cola1 + ' dona',
    cola15: products.value.cola15 + " dona",
    banana: products.value.banana + " dona",
    apple: products.value.apple + " kg",
    juice: products.value.juice + " dona",
  },
  
]
}

const buy_all =()=>{

  if(products.value.cola05 ==0 && products.value.cola1 ==0 && products.value.cola15 ==0 && products.value.banana ==0 && products.value.apple ==0 && products.value.juice ==0 ){
    all.value = 0
  }
  else{
    all.value = 7000*products.value.cola05 + 9000*products.value.cola1 + 12000*products.value.cola15 + 21000*products.value.banana + 23000*products.value.apple + 13000*products.value.juice
  }
}

onMounted(()=>{
  buy_all()
})

const dialogVisible = ref(false)

</script>

<style>
.d-flex{
  margin: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  text-align: center;
  gap: 20px;
}

.aside_{
  display: flex;
  background-color: azure;
  padding: 10px;
  gap: 5px;
  justify-content: space-between;
}
.aside_big_item{
  display: flex;
  background-color: azure;
  padding: 10px;
  gap: 5px;
}
.aside_item{
  box-shadow: rgba(0, 0, 0, 0.02) 0px 1px 3px 0px, rgba(27, 31, 35, 0.15) 0px 0px 0px 1px;
  border-radius: 5px;
  padding: 10px;
  text-align: center;
  margin: 10px 0;
  max-width: 170px;
}
.el-form-item__label {
  color: blue;
}
.product {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
}
.el_icon {
  font-size: 30px;
  background-color: rgb(45, 45, 253);
  padding: 3px;
  border-radius: 8px;
  color: rgb(255, 255, 255);
  margin-bottom: 10px;
  margin-left: 30px;
}
.buy_product {
  display: flex;
  gap: 35px;
}
.el-form-item__content {
  flex-direction: column;
}
.buy__product_item{
  margin-top: 20px;
  max-height: 300px;
  background-color: azure;
  padding: 20px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
  border-radius: 5px 0;
}

.el-text{
  font-weight: bold;
  text-align: center;
}

</style>
