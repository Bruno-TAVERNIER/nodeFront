<template>
  <div id="content">
		<h1>Projections</h1>
		<table v-show="liste.length>0">
			<thead>
				<tr>
					<th>Titre</th>
					<th>Genre</th>
					<th>Date</th>
				</tr>
			</thead>
			<tr v-for="f in liste">
				<td>{{f.titre}}</td>
				<td>{{f.genre}}</td>
				<td>{{ convert(f.date) }}</td>
			</tr>
		</table>
		<div v-show="liste.length==0">Aucun film programmé</div>
  </div>
</template>

<script>
export default{
	name: 'Projections',
	data() {
		return {
			liste: []
		}
	},
	mounted() {
		fetch('http://localhost:3000/api/programmation/'+this.$route.params.id)
		.then(res => res.json())
		.then(data => {
			this.liste = data;
		});
	},
	methods: {
		convert(dte) {
			let tabDte = dte.split('-').reverse();
			return tabDte.join('/');
		}
	}
}
</script>