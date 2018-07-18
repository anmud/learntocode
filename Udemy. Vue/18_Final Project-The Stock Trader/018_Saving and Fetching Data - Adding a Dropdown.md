# Saving and Fetching Data - Adding a Dropdown

Let's make the `dropdown` work. In our `Header` component to make the `dropdown` work we need first to add some `data`. In our `data object` let's create `isDropdownOpen` property and set it initially to `false`. In our `dropdown` in the `template` we have the `<li class="dropdown">`, if we add `open` to this class the dropdown will be opened. But our goal is dynamically add this `open` class. So, we'll use the dynamic class binding `:class="{open: isDropdownOpen}"`. So the goal now is to listen to a `click` and change this, to toggle ` isDropdownOpen` state to `true/false`. All we ned to do is to add a `click listener` to our list item  and toggle `isDropdownOpen = !isDropdownOpen`.

**Header.vue**
```html
<template>
    <nav class="navbar navbar-default">
        <div class="container-fluid">
            <div class="navbar-header">
                <router-link to="/" class="navbar-brand">Stock Trader</router-link>
            </div>

            <div class="collapse navbar-collapse">
                <ul class="nav navbar-nav">
                    <router-link to="/portfolio" activeClass="active" tag="li"><a>Portfolio</a></router-link>
                    <router-link to="/stocks" activeClass="active" tag="li"><a>Stocks</a></router-link>
                </ul>
                 <strong class="navbar-text navbar-right">Funds: {{ funds | currency }}</strong>
                <ul class="nav navbar-nav navbar-right">
                    <li><a href="#" @click="endDay">End Day</a></li>
                    <li class="dropdown" 
                    :class="{open: isDropdownOpen}"
                    @click="isDropdownOpen = !isDropdownOpen"> <!--add dynamic class, add a click listner-->
                        <a
                                href="#"
                                class="dropdown-toggle"
                                data-toggle="dropdown"
                                role="button"
                                aria-haspopup="true"
                                aria-expanded="false">Save & Load <span class="caret"></span></a>
                        <ul class="dropdown-menu">
                            <li><a href="#" >Save Data</a></li>
                            <li><a href="#" >Load Data</a></li>
                        </ul>
                    </li>
                </ul>
            </div><!-- /.navbar-collapse -->
        </div><!-- /.container-fluid -->
    </nav>
</template>

<script>
import {mapActions} from 'vuex'; 

export default{
    data(){            //create data
      return {
       isDropdownOpen: false
      }
    },
  computed:{
      funds(){
          return this.$store.getters.funds; 
      }
  },
  methods:{     
      ...mapActions([
          'randomizeStocks'
      ]),     
   endDay(){
      this.randomizeStocks();
   }
  }
}

</script>
```