<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <AppItemList title="Prefixos" v-bind:items="prefixes" v-on:addItem="addPrefix" v-on:deleteItem="deletePrefix"></AppItemList>            
          </div>
          <div class="col-md">
            <AppItemList title="Sufixos" v-bind:items="sufixes" v-on:addItem="addSufix" v-on:deleteItem="deleteSufix"></AppItemList>
          </div>
        </div>
        <br />
        <h5>Dominíos <span class="badge badge-info">{{ domains.length }}</span></h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                {{ domain }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import AppItemList from './AppItemList';

export default {
  name: "app",
  components: {
    AppItemList
  },
  data: function(){
    return {
			prefixes: ["Air", "Jet", "Flight"],
			sufixes: ["Hub", "Station", "Mart"],
			domains: ["AirHub", "AirStation", "AirMart", "JetHub", "JetStation", "JetMart", "FlightHub", "FlightStation", "FlightMart"]
		};
	},
	methods: {
		addPrefix(prefix){
      this.prefixes.push(prefix);
      this.generate();
		},
		addSufix(sufix){
      this.sufixes.push(sufix);
      this.generate();
    },
    generate() {
      this.domains = [];
      for(const prefix of this.prefixes){
        for( const sufix of this. sufixes){
          this.domains.push(prefix + sufix)
        }
      }
    },
    deletePrefix(prefix){
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
      this.generate()
    },
    deleteSufix(sufix){
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
      this.generate()
    }
	}
};
</script>

<style>

</style>
