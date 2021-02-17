<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-dark">
      <div id="nav">
        <router-link to="/User">
          <b-icon
            icon="basket2-fill"
            style="width: 30px; height: 30px"
          ></b-icon>
        </router-link>
        |
        <router-link to="/">Product</router-link>
      </div>
      <div>
        <router-link to="/User">
          <button
            type="button "
            class="btn btn-outline-success mr-1"
            @click="submit()"
          >
            ยืนยัน
          </button>
          <button
            type="button"
            class="btn btn-outline-danger"
            @click="cleardata()"
          >
            Clear
          </button>
        </router-link>
      </div>
    </nav>
    <router-view
      :Total="Total"
      :User="User"
      :Menuitem="Menuitem"
      :Data="Data"
      @Order="menuorder"
      @OrderAdmin="AddMenu"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      Total: 0,
      Menuitem: [
        {
          NameProduct: "ดินสอ2B",
          img:
            "https://www.sahachaioffice.com/wp-content/uploads/2018/01/%E0%B8%94%E0%B8%B4%E0%B8%99%E0%B8%AA%E0%B8%AD%E0%B9%80%E0%B8%82%E0%B8%B5%E0%B8%A2%E0%B8%99%E0%B9%81%E0%B8%9A%E0%B8%9A-b-5b.jpg",
          Price: 20
        },
        {
          NameProduct: "ปากกาน้ำเงิน",
          img:
            "https://www.sahachaioffice.com/wp-content/uploads/2019/03/107-600x600.jpg",
          Price: 38
        },
        {
          NameProduct: "ปากกาแดง",
          img:
            "https://aumento.officemate.co.th/media/catalog/product/O/F/OFM1030212.jpg?imwidth=640",
          Price: 6
        },
        {
          NameProduct: "ลิควิด",
          img:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSIcJah2hdgjaI4FYLpL0g4paVzgSii_Z7gkH8CaO-0Tge5pOj8mRe6DRdvtSQmwEsZVrIn83x6&usqp=CAc",
          Price: 55
        },
        {
          NameProduct: "สมุดโน๊ต",
          img:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQCNrwZEXw1EVD5zbVNxT4Lc3hAAZepl9U-XCjXnJiUgsfo6f2taEFKR6pp7TfILBMzrfiZUKd0&usqp=CAc",
          Price: 50
        },
        {
          NameProduct: "ไม้บรรทัด",
          img:
            "data:image/jpeg;base64,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",
          Price: 40
        },
        {
          NameProduct: "ยางลบ",
          img:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ29Z0e6HDyESbHkFHp3Agkm6N9RTFdy1yRbndUte1Chtweoa2zBrcSsYW_EW54KCzufByt1RWNew&usqp=CAc",
          Price: 5
        },
        {
          NameProduct: "โบ้",
          img:
            "https://cdn.readawrite.com/publicassets/484067/images/4572E9B4-A023-4DFD-820F-1FE75C0473BA.jpeg",
          Price: 0
        }
      ],
      select: [],
      Data: []
    };
  },
  methods: {
    //คิดยอดรวมทั้งหมด
    submit() {
      this.Data = this.select;
      this.Total = 0;
      for (var i = 0; i < this.Data.length; i++) {
        this.Total = this.Total + this.Data[i].Total;
      }
    },
    cleardata() {
      this.Total = 0;
      this.Data = [{}];
      this.select = [{}];
    },
    menuorder(value) {
      this.select = value;
    },
    AddMenu(value) {
      this.Menuitem.push(value);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 10px;
}

#nav a {
  font-weight: bold;
  color: #ffffff;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
