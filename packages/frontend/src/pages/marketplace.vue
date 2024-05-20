<!--
SPDX-FileCopyrightText: syuilo and misskey-project
SPDX-License-Identifier: AGPL-3.0-only
-->

<template>
<MkStickyContainer>
	<template #header><MkPageHeader v-model:tab="tab" :actions="headerActions"/></template>
	<XUsers/>
</MkStickyContainer>
</template>

<script lang="ts" setup>
import { computed, watch, ref, shallowRef } from 'vue';
import XUsers from './explore.users.vue';
import MkFoldableSection from '@/components/MkFoldableSection.vue';
import { definePageMetadata } from '@/scripts/page-metadata.js';
import { i18n } from '@/i18n.js';

const props = withDefaults(defineProps<{
        tag?: string;
        initialTab?: string;
    }>(), {
	initialTab: 'marketplace',
});

const tab = ref(props.initialTab);
const tagsEl = shallowRef<InstanceType<typeof MkFoldableSection>>();

watch(() => props.tag, () => {
	if (tagsEl.value) tagsEl.value.toggleContent(props.tag == null);
});

const headerActions = computed(() => []);

definePageMetadata(() => ({
	title: i18n.ts.marketplace,
	icon: 'ti ti-shopping-cart',
}));
</script>
