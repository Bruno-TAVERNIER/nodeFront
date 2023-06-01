<template>
  <div id="content">
		<h1>{{ $route.params.id ? 'Modifier':'Ajouter'}} un cinéma</h1>
		<form @submit.prevent="go">
			<p>
				<label>Nom</label>
				<input v-model="infos.nom" type="text" />
			</p>
			<p>
				<label>Adresse</label>
				<input v-model="infos.adresse" type="text" />
			</p>
			<p>
				<input type="submit" value="Enregistrer" />
			</p>
		</form>
  </div>
</template>

<script>
export default{
	name: 'FormCine',
	data() {
		return {
			infos: {nom: '', adresse: ''}
		}
	},
	mounted() {
		if(this.$route.params.id){
			fetch('http://localhost:3000/api/'+this.$route.params.id)
			.then(res => res.json())
			.then((data) => {
				console.log(data);
				this.infos = data[0];
		});
		}
	},
	methods: {
		go(){
			//transformation Objet en url correcte
			var data = new URLSearchParams(this.infos).toString();
			//modif
			if(this.infos.num_cine){
				fetch('http://localhost:3000/api/up/'+this.infos.num_cine, {
  				method: 'PUT',
					headers: {
						'Content-Type' : 'application/x-www-form-urlencoded',
					},
					mode: 'cors',
  				body: data
				})
				.then(res => res.json())
				.then(retour => {
					console.log(retour);
					this.$router.replace('/');
				});
			}
			//ajout
			else {
				fetch('http://localhost:3000/api/add', {
  				method: 'POST',
					headers: {
						'Content-Type' : 'application/x-www-form-urlencoded',
					},
					mode: 'cors',
  				body: data
				})
				.then(res => res.json())
				.then(data => {
					console.log(data);
					this.$router.replace('/');
				});
			}
		}
	}
}
</script>