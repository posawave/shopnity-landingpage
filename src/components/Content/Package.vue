<template>
  <div class="layout-container" id="top-of-content">
    <el-row :gutter="24" justify="center" align="middle" class="no-margin">
      <el-col :xs="24" :sm="10" :md="10" :lg="10" :xl="10">
        <img src="" alt="">
      </el-col>
      <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8" style="min-height: 100px;">
        <div v-for="(item, index) in !isPro ? descBasic : descPro" :key="index">
          <span v-html="item"></span>
        </div>
      </el-col>
      <el-col :xs="24" :sm="6" :md="6" :lg="6" :xl="6" style="min-height: 100px;">
        <el-button type="primary" :class="!isPro ? 'gredient-button' : 'gredient-button-pro'">{{!isPro ? 'สมัครระบบฟรี ตลอดไป' : 'สมัครวันนี้ ใช้งานฟรี 15 วัน'}}</el-button>
      </el-col>
    </el-row>
    <!-- Package list -->
    <el-row justify="space-around" align="middle">
      <el-col style="padding: 10px" :xs="24" :sm="12" :md="6" :lg="6" :xl="6" v-for="(item, idx) in isPro ? pro : basic" :key="idx">
        <div class="package-container">
          <div style="font-size: 17px; color: black;">
            {{item.title}}
          </div>
          <div style="font-size: 17px; color: black;">
            {{item.price}} ฿
          </div>
          <div>
            <span style="font-size: 12px; color: white; background-color: #555; padding: 5px; margin: 0 8px;" v-for="(pitem, ind) in item.pricePack" :key="ind">{{pitem}}</span>
          </div>
          <div style="height: 20px; padding: 28px 0 15px 0;">
            <button v-if="item.isBuyable" class="package-buyable-btn">
              Buy
            </button>
          </div>
          <div v-for="(dItem, index) in item.detail" :key="index" class="package-detail-list">
            {{dItem}}
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col style="text-align: center; margin: 20px 0">
        <span class="text-isPro" :style="!isPro ? 'color: #009df8;' : ''">
          รุ่นธรรมดา
        </span>
        <label class="switch">
          <input @click="scrollToTop" type="checkbox" v-model="isPro" checked>
          <span class="slider round"></span>
        </label>
        <span class="text-isPro" :style="isPro ? 'color: #009df8;' : ''">
          รุ่น Pro
        </span>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'Title',
  data () {
    return {
      isPro: false,
      descBasic: [
        '<span class="package-title-text">สมัครวันนี้ ฟรีทันที 50 ออร์เดอร์</span>',
        '<span class="package-title-text">- ใช้งานฟรีตลอดไป</span>',
        '<span class="package-title-text">- ไม่จำกัดฟีเจอร์</span>',
        '<span class="package-title-text">- ขายของครบเครื่องทุกฟังก์ชัน</span>'
      ],
      descPro: [
        '<span class="package-title-head-pro">Shipnity Pro มีอะไรพิเศษกว่า?</span>',
        '- <span class="package-title-text-pro">ระบบ POS ขายของหน้าร้าน</span>',
        '- <span class="package-title-text-pro">ประวัติการสั่งซื้อ</span>ของลูกค้าแต่ละคน',
        '- <span class="package-title-text-pro">ต้นทุนสินค้า</span>เปลี่ยนตามล็อต',
        '- <span class="package-title-text-pro">ประวัติ Supplier</span>ทั้งรายการขายและรายการสั่งซื้อ',
        '- <span class="package-title-text-pro">ทำออเดอร์อย่างเป็นระบบ</span>',
        '- <span>(1.เปิดออเดอร์ 2.ตรวจสอบการแจ้งเตือน 3.แพ็คของ)</span>',
        '- ยิงบาร์โค็ดสินค้าเพื่อ <span class="package-title-text-pro">เช็คของก่อนแพ็คส่ง</span> ป้องกันการตกหล่นหรือหยิบผิด',
        '- <span class="package-title-text-pro">ระบบคืนสินค้า/สินค้าชำรุด</span>',
        '- <span class="package-title-text-pro">รายงาน Cash Flow</span> ของร้าน'
      ],
      basic: [
        {
          title: 'เริ่มต้น',
          price: 0,
          isBuyable: false,
          pricePack: [
            'ฟรีตลอดไป'
          ],
          detail: [
            '50 ออเดอร์/เดือน',
            '1 Admin',
            '1 คลังสินค้า',
            '0 ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
        {
          title: 'ร้านขนาดกลาง',
          price: 450,
          isBuyable: true,
          pricePack: [
            '1200 บาท / 3 เดือน',
            '4700 บาท / 1 ปี',
          ],
          detail: [
            '150 ออเดอร์/เดือน',
            '3 Admin',
            '1 คลังสินค้า',
            '4 ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
        {
          title: 'ร้านขนาดใหญ่',
          price: 650,
          isBuyable: true,
          pricePack: [
            '1800 บาท / 3 เดือน',
            '6900 บาท / 1 ปี',
          ],
          detail: [
            '300 ออเดอร์/เดือน',
            '6 Admin',
            '1 คลังสินค้า',
            '8 ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
        {
          title: 'ไม่จำกัด',
          price: 850,
          isBuyable: true,
          isBuyable: true,
          pricePack: [
            '6900 บาท / 3 เดือน',
            '8900 บาท / 1 ปี',
          ],
          detail: [
            'ไม่จำกัด ออเดอร์/เดือน',
            '10 Admin',
            '1 คลังสินค้า',
            '10 ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
      ],
      pro: [
        {
          title: 'Quiet Pro',
          price: 890,
          isBuyable: true,
          pricePack: [
            '2600 บาท / 3 เดือน',
            '8900 บาท / 1 ปี',
          ],
          detail: [
            'ไม่จำกัด ออเดอร์/เดือน',
            '10 Admin',
            '1 คลังสินค้า',
            '0 ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
        {
          title: 'Pro',
          price: 1190,
          isBuyable: true,
          pricePack: [
            '3400 บาท / 3 เดือน',
            '11900 บาท / 1 ปี',
          ],
          detail: [
            'ไม่จำกัด ออเดอร์/เดือน',
            '15 Admin',
            '2 คลังสินค้า',
            '15 ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
        {
          title: 'Truely Pro',
          price: 1590,
          isBuyable: true,
          pricePack: [
            '4600 บาท / 3 เดือน',
            '15900 บาท / 1 ปี',
          ],
          detail: [
            'ไม่จำกัด ออเดอร์/เดือน',
            '20 Admin',
            '3 คลังสินค้า',
            '30 ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
        {
          title: 'Extreamly Pro',
          price: 1990,
          isBuyable: true,
          pricePack: [
            '5800 บาท / 3 เดือน',
            '19900 บาท / 1 ปี',
          ],
          detail: [
            'ไม่จำกัด ออเดอร์/เดือน',
            'ไม่จำกัด Admin',
            'ไม่จำกัด คลังสินค้า',
            'ไม่จำกัด ตัวแทนจำหน่าย',
            'ไม่จำกัด รายการสินค้า'
          ]
        },
      ]
    }
  },
  methods: {
    scrollToTop () {
      document.getElementById('top-of-content').scrollIntoView({behavior: "smooth", block: "start", inline: "start"});;
    }
  }
};
</script>

<style lang="scss">
  .no-margin {
    margin: 0!important;
  }

  .switch {
    position: relative;
    display: inline-block;
    width: 100px;
    height: 28px;
  }

  .switch input { 
    opacity: 0;
    width: 0;
    height: 0;
  }

  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: linear-gradient(#00d6cb, #009df8);
    -webkit-transition: .4s;
    transition: .4s;
  }

  .slider:before {
    position: absolute;
    content: "";
    height: 21px;
    width: 21px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: .4s;
    transition: .4s;
  }

  input:checked + .slider {
    background-image: linear-gradient(#00d6cb, #009df8);
  }

  input:focus + .slider {
    box-shadow: 0 0 1px #2196F3;
  }

  input:checked + .slider:before {
    -webkit-transform: translateX(71px);
    -ms-transform: translateX(71px);
    transform: translateX(71px);
  }

  /* Rounded sliders */
  .slider.round {
    border-radius: 34px;
  }

  .slider.round:before {
    border-radius: 50%;
  }

  .layout-container {
    background-color: white;
    margin: 20px 0 0 0;
    padding: 24px 0 24px 0;
  }

  .package-title-text {
    min-height: 100px;
    color: rgb(0, 146, 127);
  }

  .package-title-head-pro {
    color: #3366FF;
    font-size: 18px;
    font-weight: bold;
  }

  .package-title-text-pro {
    color: #009df8;
  }

  .gredient-button {
    background-image: linear-gradient(#00d6cb, #009df8);
    border: none;

    &:hover {
      background-image: linear-gradient(#00e2d7, #3eb8ff);
    }
    &:active {
      background-image: linear-gradient(#00d6cb, #009df8);
    }
    &:focus {
      background-image: linear-gradient(#00d6cb, #009df8);
    }
  }
  
  .gredient-button-pro {
    background-image: linear-gradient(#3399FF, #47bbff);
    border: none;

    &:hover {
      background-image: linear-gradient(#0063f8, #3eb8ff);
    }
    &:active {
      background-image: linear-gradient(#3399FF, #47bbff);
    }
    &:focus {
      background-image: linear-gradient(#3399FF, #47bbff);
    }
  }
  
  .package-card {
    border: 0.1px #aaa solid;
  }

  .package-container {
    padding: 15px 10px;
    border: 1px solid #ccc;
    text-align: center;
  }

  .package-detail-list {
    margin: 15px 20px 15px 20px;
    border-bottom: 1px solid #ccc;
    color: rgb(0, 146, 127);
  }

  .package-buyable-btn {
    position: relative;
    background-color: Transparent;
    background-repeat:no-repeat;
    font-size: 15px;
    font-weight: bold; 
    color: rgb(0, 146, 127);
    border: rgb(0, 146, 127) 1px solid;
    border-radius: 17px;
    padding: 7px 45px;
    outline: none;
    background: none;
    overflow:hidden;
    z-index: 1;
    cursor: pointer;
    transition:         0.08s ease-in;
    -o-transition:      0.08s ease-in;
    -ms-transition:     0.08s ease-in;
    -moz-transition:    0.08s ease-in;
    -webkit-transition: 0.08s ease-in;

    &:hover {
      color: white;
      border: rgb(0, 182, 158) 1px solid;
    }

    &:before {
      content: "";
      position: absolute;
      background: rgb(0, 182, 158);
      bottom: 0;
      left: 0;
      right: 0;
      top: 100%;
      z-index: -1;
      -webkit-transition: top 0.09s ease-in;
    }

    &:hover:before {
      top: 0;
    }
  }

  .text-isPro {
    margin: 0 20px;
  }
</style>
