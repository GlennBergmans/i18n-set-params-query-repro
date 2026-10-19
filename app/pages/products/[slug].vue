<script lang="ts" setup>
const setI18nParams = useSetI18nParams();
setI18nParams({ en: { slug: "red-mug" }, nl: { slug: "rode-mok" }, ja: { slug: "akai-magu" } });
</script>

<template>
	<div>
		<h1>{{ $route.params.slug }}</h1>
	</div>
</template>
