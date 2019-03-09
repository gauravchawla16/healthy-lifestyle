<template>
  <div class="d-flex flex-column">
    <h3>Search for the product to know more</h3>
    <el-row type="flex" align="middle" class="justify-content-center">
       <el-autocomplete v-model="state4" :fetch-suggestions="querySearchAsync" placeholder="Start typing" @select="handleSelect"></el-autocomplete>
    </el-row>
    <el-row type="flex" align="middle" class="justify-content-center" v-if="Object.keys(product).length > 0">
      <component-detail :item="product"></component-detail>
    </el-row>
  </div>
</template>

<script>
// @ is an alias to /src
import { Autocomplete, Row } from 'element-ui'
import ComponentDetail from '@/components/ComponentDetail.vue'

export default {
  name: 'home',
  components: {
    ComponentDetail,
    'el-row': Row,
    'el-autocomplete': Autocomplete
  },
  data () {
    return {
      links: [],
      state4: '',
      product: {}
    }
  },
  methods: {
    loadAll () {
      return [
        { 'value': 'Black Forest Ham', 'calories': 290, 'correctedTerm': '6 inch Black Forest Ham' },
        { 'value': 'Black Forrest Ham', 'calories': 290, 'correctedTerm': '6 inch Black Forest Ham' },
        { 'value': 'Six inch Black Forest Ham', 'calories': 290 },
        { 'value': '6 inch Black Forest Ham', 'foodType': 'Six inch', 'calories': 290 },
        { 'value': '12 inch Black Forest Ham', 'calories': 580 },
        { 'value': 'Footlong Black Forest Ham', 'foodType': 'Footlong', 'calories': 580 },
        { 'value': 'Oven Roasted Chicken', 'calories': 320 },
        { 'value': '6 inch Oven Roasted Chicken', 'foodType': 'Six inch', 'calories': 320 },
        { 'value': 'Six inch Oven Roasted Chicken', 'calories': 320 },
        { 'value': '12 inch Oven Roasted Chicken', 'calories': 640 },
        { 'value': 'Footlong Oven Roasted Chicken', 'foodType': 'Footlong', 'calories': 640 },
        { 'value': '6 inch Roast Beef', 'foodType': 'Six inch', 'calories': 320 },
        { 'value': 'Six inch Roast Beef', 'calories': 320 },
        { 'value': '12 inch Roast Beef', 'calories': 640 },
        { 'value': 'Footlong Roast Beef', 'foodType': 'Footlong', 'calories': 640 },
        { 'value': 'Rotisserie-Style Chicken', 'calories': 350 },
        { 'value': 'Roasted Chicken', 'calories': 350 },
        { 'value': 'Rotisserie Chicken', 'foodType': 'Chicken', 'calories': 350 },
        { 'value': '6 inch Rotisserie Chicken', 'foodType': 'Six inch', 'calories': 350 },
        { 'value': 'Six inch Rotisserie Chicken', 'calories': 350 },
        { 'value': '12 inch Rotisserie Chicken', 'calories': 700 },
        { 'value': 'Footlong Rotisserie Chicken', 'foodType': 'Footlong', 'calories': 700 },
        { 'value': 'Rotisserie Chicken Sandwich', 'calories': 350 },
        { 'value': 'Subway Club', 'calories': 310, 'correctedTerm': '6 inch Subway Club' },
        { 'value': '6 inch Subway Club', 'foodType': 'Six inch', 'calories': 310 },
        { 'value': '12 inch Subway Club', 'calories': 620 },
        { 'value': 'Footlong Subway Club', 'calories': 620 },
        { 'value': 'Chicken Teriyaki', 'calories': 370, 'correctedTerm': '6 inch Sweet Onion Chicken Teriyaki' },
        { 'value': '6 inch Chicken Teriyaki', 'calories': 370, 'correctedTerm': '6 inch Sweet Onion Chicken Teriyaki' },
        { 'value': 'Sweet Onion Chicken Teriyaki', 'calories': 370, 'correctedTerm': '6 inch Sweet Onion Chicken Teriyaki' },
        { 'value': '6 inch Sweet Onion Chicken Teriyaki', 'foodType': 'Six inch', 'calories': 370 },
        { 'value': '12 inch Sweet Onion Chicken Teriyaki', 'calories': 740 },
        { 'value': 'Footlong Teriyaki Chicken', 'calories': 740 },
        { 'value': 'Footlong Sweet Onion Chicken Teriyaki', 'calories': 740 },
        { 'value': 'Turkey Breast', 'foodType': 'Turkey', 'calories': 280, 'correctedTerm': '6 inch Turkey Breast' },
        { 'value': '6 inch Turkey and Cheese', 'calories': 280 },
        { 'value': 'Six inch Turkey and Cheese', 'calories': 280 },
        { 'value': '6 inch Turkey Breast', 'foodType': 'Six inch', 'calories': 280 },
        { 'value': '12 inch Turkey Breast', 'calories': 560 },
        { 'value': 'Footlong Turkey Breast', 'calories': 560 },
        { 'value': 'Foot long Turkey', 'calories': 560, 'correctedTerm': 'Footlong Turkey Breast' },
        { 'value': 'Veggie Delite', 'calories': 280, 'correctedTerm': '6 inch Veggie Delite' },
        { 'value': 'Veggie Delight', 'calories': 280, 'correctedTerm': '6 inch Veggie Delite' },
        { 'value': '6 inch Veggie Delite', 'foodType': 'Six inch', 'calories': 280 },
        { 'value': 'Six inch Veggie Delite', 'calories': 280, 'correctedTerm': '6 inch Veggie Delite' },
        { 'value': '6 inch Veggie Delight', 'calories': 280, 'correctedTerm': '6 inch Veggie Delite' },
        { 'value': '12 inch Veggie Delite', 'calories': 560 },
        { 'value': 'Footlong Veggie Delite', 'calories': 560 },
        { 'value': 'Carved Turkey', 'foodType': 'Turkey', 'calories': 330 },
        { 'value': '6 inch Carved Turkey', 'foodType': 'Turkey', 'calories': 330 },
        { 'value': '12 inch Carved Turkey', 'foodType': 'Turkey', 'calories': 660 },
        { 'value': 'Footlong Carved Turkey', 'foodType': 'Turkey', 'calories': 660 },
        { 'value': 'Chicken and Bacon Ranch Melt', 'foodType': 'Chicken', 'calories': 590 },
        { 'value': 'Chicken Bacon Ranch Melt', 'foodType': 'Chicken', 'calories': 590 },
        { 'value': 'Cold Cut Combo', 'calories': 340 },
        { 'value': 'Cold Cut', 'calories': 340 },
        { 'value': '6 inch Cold Cut Combo', 'foodType': 'Six inch', 'calories': 340 },
        { 'value': '12 inch Cold Cut Combo', 'calories': 680 },
        { 'value': 'Footlong Cold Cut Combo', 'calories': 680 },
        { 'value': 'Italian BMT', 'calories': 390, 'correctedTerm': '6 inch Italian BMT' },
        { 'value': 'BMT', 'calories': 390, 'correctedTerm': '6 inch Italian BMT' },
        { 'value': '6 inch Italian BMT', 'foodType': 'Six inch', 'calories': 390 },
        { 'value': '12 inch Italian BMT', 'calories': 780 },
        { 'value': 'Footlong Italian BMT', 'calories': 780 },
        { 'value': 'Meatball Marinara', 'calories': 460 },
        { 'value': '6 inch Meatball Marinara', 'calories': 460 },
        { 'value': '12 inch Meatball Marinara', 'calories': 920 },
        { 'value': 'Footlong Meatball Marinara', 'calories': 920 },
        { 'value': 'Meatball Sub', 'calories': 460, 'correctedTerm': '6 inch Meatball Sub' },
        { 'value': '6 inch Meatball Sub', 'calories': 460 },
        { 'value': '6 inch Meatball', 'calories': 460, 'correctedTerm': '6 inch Meatball Sub' },
        { 'value': '12 inch Meatball Sub', 'calories': 920 },
        { 'value': 'Footlong Meatball Sub', 'calories': 920 },
        { 'value': 'Spicy Italian', 'calories': 470, 'correctedTerm': '6 inch Spicy Italian' },
        { 'value': '6 inch Spicy Italian', 'calories': 470 },
        { 'value': '12 inch Spicy Italian', 'calories': 940 },
        { 'value': 'Footlong Spicy Italian', 'calories': 940 },
        { 'value': 'Spicy Italian Footlong', 'calories': 940, 'correctedTerm': 'Footlong Spicy Italian' },
        { 'value': 'Spicy Italian Sub', 'calories': 470 },
        { 'value': 'Steak and Cheese', 'calories': 470, 'correctedTerm': '6 inch Steak and Cheese' },
        { 'value': 'Philly Cheese Steak', 'calories': 470, 'correctedTerm': '6 inch Steak and Cheese' },
        { 'value': '6 inch Steak and Cheese', 'calories': 470 },
        { 'value': '12 inch Steak and Cheese', 'calories': 940 },
        { 'value': 'Footlong Steak and Cheese', 'calories': 940 },
        { 'value': 'Tuna', 'calories': 470 },
        { 'value': '6 inch Tuna', 'calories': 470 },
        { 'value': '12 inch Tuna', 'calories': 940 },
        { 'value': 'Footlong Tuna', 'calories': 940 },
        { 'value': 'Italian Hero', 'calories': 550 },
        { 'value': '6 inch Italian Hero', 'calories': 550 },
        { 'value': '12 inch Italian Hero', 'calories': 1100 },
        { 'value': 'Footlong Italian Hero', 'calories': 1100 },
        { 'value': 'Black Forest Ham Salad', 'calories': 110, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Oven Roasted Chicken Salad', 'calories': 150, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Roast Beef Salad', 'foodType': 'Salad', 'calories': 140, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Rotisserie-Style Chicken Salad', 'calories': 170, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Rotisserie Chicken Salad', 'foodType': 'Salad', 'calories': 170, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Subway Club Salad', 'calories': 140, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Sweet Onion Chicken Teriyaki Salad', 'calories': 230, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Turkey Breast Salad', 'foodType': 'Salad', 'calories': 110, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Veggie Delite Salad', 'foodType': 'Salad', 'calories': 60, 'sideItem': true, 'dressingItem': true },
        { 'value': 'Bacon, Egg & Cheese', 'calories': 460 },
        { 'value': 'Bacon, Egg & Cheese Sandwich', 'calories': 460 },
        { 'value': 'Ham, Egg & Cheese', 'calories': 410 },
        { 'value': 'Ham, Egg & Cheese Sandwich', 'calories': 410 },
        { 'value': 'Black Forest Ham, Egg & Cheese', 'calories': 410 },
        { 'value': 'Black Forest Ham, Egg & Cheese Sandwich', 'calories': 410 },
        { 'value': 'Egg & Cheese', 'calories': 380 },
        { 'value': 'Egg & Cheese Sandwich', 'calories': 380 },
        { 'value': 'Steak, Egg & Cheese', 'calories': 450 },
        { 'value': 'Steak, Egg & Cheese Sandwich', 'calories': 450 },
        { 'value': 'Salt and Vinegar Chips', 'calories': 230, 'sideItem': true },
        { 'value': 'Baked BBQ', 'calories': 130, 'sideItem': true },
        { 'value': 'Baked BBQ Chips', 'calories': 130, 'sideItem': true },
        { 'value': 'Baked Barbeque', 'calories': 130, 'sideItem': true },
        { 'value': 'Baked Barbeque Chips', 'calories': 130, 'sideItem': true },
        { 'value': 'Chips', 'calories': 160, 'sideItem': true },
        { 'value': 'Apple Slices', 'calories': 35, 'sideItem': true },
        { 'value': 'Apple', 'calories': 35, 'sideItem': true, 'correctedTerm': 'Apple Slices' },
        { 'value': 'Potato Chips', 'calories': 160, 'sideItem': true },
        { 'value': 'Potato Chip', 'calories': 160, 'sideItem': true },
        { 'value': 'Lays Potato Chips', 'calories': 160, 'sideItem': true },
        { 'value': 'Doritos', 'calories': 140, 'sideItem': true },
        { 'value': 'Doritos Nacho Cheese Tortilla Chips', 'calories': 140, 'sideItem': true },
        { 'value': 'Cheetos', 'calories': 150, 'sideItem': true },
        { 'value': 'Hot Cheetos', 'calories': 150, 'sideItem': true },
        { 'value': 'Beef Chili with Beans', 'foodType': 'Soup', 'calories': 360, 'sideItem': true },
        { 'value': 'Black Bean Soup', 'foodType': 'Soup', 'calories': 210, 'sideItem': true },
        { 'value': 'Broccoli Cheddar Soup', 'foodType': 'Soup', 'calories': 170, 'sideItem': true },
        { 'value': 'Chicken Tortilla Soup', 'calories': 110, 'sideItem': true },
        { 'value': 'Creamy Chicken & Dumpling Soup', 'calories': 150, 'sideItem': true },
        { 'value': 'Creamy Chicken & Wild Rice Soup', 'calories': 190, 'sideItem': true },
        { 'value': 'French Onion Soup', 'foodType': 'Soup', 'calories': 150, 'sideItem': true },
        { 'value': 'Homestyle Chicken Noodle Soup', 'calories': 110, 'sideItem': true },
        { 'value': 'Chicken Noodle Soup', 'calories': 110, 'sideItem': true },
        { 'value': 'Loaded Baked Potato with Bacon Soup', 'calories': 210, 'sideItem': true },
        { 'value': 'Tomato Basil Soup', 'foodType': 'Soup', 'calories': 130, 'sideItem': true },
        { 'value': 'Raspberry Cheesecake Cookie', 'calories': 200, 'sideItem': true },
        { 'value': 'White Chip Macadamian Nut Cookie', 'calories': 220, 'sideItem': true },
        { 'value': 'Chocolate Chunk Cookie', 'calories': 210, 'sideItem': true },
        { 'value': 'Double Chocolate Cookie', 'calories': 210, 'sideItem': true }
      ]
    },
    querySearchAsync (queryString, cb) {
      var links = this.links
      var results = queryString ? links.filter(this.createFilter(queryString)) : links
      cb(results)
    },
    createFilter (queryString) {
      return (link) => {
        return (link.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0)
      }
    },
    handleSelect (item) {
      this.product = item
    }
  },
  mounted () {
    this.links = this.loadAll()
  }
}
</script>
<style>
.el-input{
  width: 500px !important;
}
</style>
