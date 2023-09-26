<script setup lang="ts">
	import { ref } from 'vue';
	const form = ref({
		email: '',
		password: '',
		remember: false,
	});

	const isLoading = ref(false);

	function submit() {
		if (!form.value.email) {
			return;
		}

		isLoading.value = true;

		setTimeout(() => {
			isLoading.value = false;
			alert(JSON.stringify(form.value));
		}, 3000);
	}

	const rules = {
		required: (value: any) => !!value || 'Campo é obrigatório',
		counter: (value: any) => value.length >= 6 || 'Senha deve ter no mínimo 6 caracteres',
		email: (value: any) => {
			const pattern =
				/^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/;
			return pattern.test(value) || 'Deve ser um email válido';
		},
	};
</script>

<template>
	<v-container fluid>
		<v-overlay
			:model-value="isLoading"
			class="align-center justify-center"
		>
			<v-progress-circular
				size="64"
				v-if="isLoading"
				indeterminate
				color="white"
			></v-progress-circular>
		</v-overlay>
		<v-row class="justify-center">
			<v-col
				cols="9"
				sm="8"
				md="6"
				lg="4"
				xl="3"
			>
				<v-card class="pa-4">
					<v-card-title class="text-center">Login</v-card-title>
					<v-card-item>
						<v-form @submit.prevent="submit">
							<v-text-field
								prepend-inner-icon="mdi-email"
								v-model="form.email"
								label="Email"
								:rules="[rules.required, rules.email]"
							></v-text-field>

							<v-text-field
								type="password"
								prepend-inner-icon="mdi-key"
								v-model="form.password"
								label="Password"
								:rules="[rules.required, rules.counter]"
							></v-text-field>

							<v-checkbox
								v-model="form.remember"
								label="Lembrar-se de mim"
								color="red"
								hide-details
							></v-checkbox>
							<v-btn
								variant="elevated"
								color="red-darken-1"
								type="submit"
								block
								class="mt-2"
							>
								Entrar
							</v-btn>
						</v-form>
					</v-card-item>

					<v-card-action>
						<div class="mx-4">
							<v-btn
								block
								to="registrar"
								>Registrar</v-btn
							>
						</div>
					</v-card-action>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>
