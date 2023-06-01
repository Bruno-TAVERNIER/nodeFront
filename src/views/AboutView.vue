<template>
  <div id="content">
    <h1>Crédits</h1>
    <ul>
      <li v-for="cd in liste">
        <a :href="cd.url" target="_blank">{{ cd.name }}</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default{
	name: 'About',
	data() {
		return {
			liste: [
        {id: 1, url: 'http://vuejs.org', name: 'Vue JS'},
        {id: 2, url: 'http://router.vuejs.org', name: 'Vue JS Router'},
        {id: 3, url: 'http://nodejs.org', name: 'Node JS'},
        {id: 4, url: 'https://www.npmjs.com/package/mysql', name: 'Module MySQL for Node'},
        {id: 5, url: 'https://expressjs.com/fr/', name: 'Express JS'},
        {id: 6, url:'#', name: 'Et beaucoup d\'autres'}
      ]
		}
	}
}
</script>

<style scoped>
ul {
  list-style-type: none;
  font-size: 1.5em;
}
li {
  border: 1px solid silver;
  text-align: center;
  margin-bottom: 10px;
  border-radius: 20px;
}

</style>