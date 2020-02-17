<template>
	<li>
		<span>{{item.id}})</span>
		<template v-if="!isEditMode">
			<span class="fix-width">{{item.text}}</span>
			<input type="button" value="ред." @click="isEditMode = true"/>
			<input type="button" value="Х" @click="$emit('delete-item', item.id)"/>
		</template>
		<template v-else>
			<input class="fix-width" type="text" v-model="newText" />
			<input type="button" value="ок" @click="editItem"/>
			<input type="button" value="отмена" @click="cancel"/>
		</template>
	</li>
</template>

<script>
    export default {
        name: "Item",
		props: ['item'],
		data() {
            return {
                isEditMode: false,
				newText: this.item.text
			}
        },
		methods: {
            editItem() {
                this.isEditMode = false;
                this.$emit('edit-item', {id: this.item.id, text: this.newText});
			},
			cancel() {
                this.isEditMode = false;
                this.newText = this.item.text;
			}
		}
    }
</script>

<style scoped>
	span {
		margin-right: 5px;
	}
	.fix-width {
		width: 200px;
		display: inline-block;
		overflow-wrap: break-word;
		vertical-align: middle;
	}
</style>