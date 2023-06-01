<template>
  <div id="content">
		<h1>Liste des cinémas</h1>
		<table v-show="liste.length>0">
			<thead>
				<tr>
					<th>Numéro</th>
					<th>Cinéma</th>
					<th>Ville</th>
					<th>Action</th>
				</tr>
			</thead>
			<tr v-for="c in liste">
				<td>{{c.num_cine}}</td>
				<td><router-link :to="{name: 'projections', params: {id: c.num_cine }}">{{c.nom}}</router-link></td>
				<td>{{c.adresse}}</td>
				<td>
					<router-link :to="{name: 'edit', params: {id: c.num_cine }}">Edit</router-link> - 
					<a @click="del(c.num_cine)">Effacer</a>
				</td>
			</tr>
		</table>
		<div v-show="liste.length==0">Aucun cinéma à afficher</div>
  </div>
</template>

<script>
export default{
	name: 'Home',
	data() {
		return {
			liste: []
		}
	},
	mounted() {
		fetch('http://localhost:3000/api')
		.then(res => res.json())
		.then(data => {
			this.liste = data;
		});
	},
	methods: {
		del(id){
			fetch('http://localhost:3000/api/supp/'+id, {
				method: 'delete'
			})
			.then(res => res.json())
			.then(data => {
				if(data.err) alert(data.err);
				else {
					alert(data.msg);
					this.liste = data.liste;
				}
			});
		}
	}
}
</script>