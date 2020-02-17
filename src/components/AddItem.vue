<template>
	<div>
		<span class="red block" v-if="error">Не удалось добавить элемент</span>
		<label>
			Новый элемент:
			<input class="block" type="text" placeholder="текст элемента" v-model="text" />
		</label>
		<input type="button" value="Добавить" @click="addItem"/>
	</div>
</template>

<script>
    export default {
        name: "AddItem",
		data() {
            return {
                text: '',
				error: false
			}
		},
		methods: {
            addItem() {
                if (this.text !== '') {
                    this.$emit('add-item', this.text);
                    this.text = '';
				} else {
                    this.error = true;
                    setTimeout(() => this.error = false, 1000);
				}
			}
		}
    }
</script>

<style scoped>
	.block {
		display: block;
		margin-bottom: 10px;
	}
	.red {
		color: red;
	}
</style>