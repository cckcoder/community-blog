<template>
	<div class="row my-5">
		<div class="col-md-6 offset-md-3">
			<div class="card">
				<div class="card-body">
					<h3 class="text-center my-4">Signup</h3>

					<div class="form-group">
						<input v-model="name" class="form-control" placeholder="Name" type="TEXT">
						<div class="errors" v-if="errors.name">
							<small class="text-danger" :key="error" v-for="error in errors.name">{{ error }}</small>
						</div>
					</div>

					<div class="form-group">
						<input v-model="email" class="form-control" placeholder="Email" type="TEXT">
						<div class="errors" v-if="errors.email">
							<small class="text-danger" :key="error" v-for="error in errors.email">{{ error }}</small>
						</div>
					</div>

					<div class="form-group">
						<input v-model="password" class="form-control" placeholder="Password" type="PASSWORD">
					</div>

					<div class="form-group text-center">
						<button @click="registerUser()" class="btn btn-success form-control">Signup</button>
					</div>

				</div>
			</div>
		</div>
	</div>
</template>


<script>
import Axios from 'axios'

export default {
	data() {
		return {
			name: '',
			email: '',
			password: '',
			errors: {}
		}
	},
	methods: {
		registerUser() { 
			console.log('Call...')
			Axios.post('https://react-blog-api.bahdcasts.com/api/auth/register', {
				name: this.name,
				email: this.email,
				password: this.password,
			}).then((response) => { 
				const { data } = response.data;
				localStorage.setItem('auth', JSON.stringify(data))
				this.$root.auth = data
				this.$router.push('home')
			}).catch(response => {
				this.errors = response.data
				console.log(response) 
			})
		}
	}
}
</script>