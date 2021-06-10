<!--
  Copyright 2020 Hippo B.V. (http://www.onehippo.com)

  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
  -->

<template>
  <div v-if="document" :class="{ 'has-edit-button': page.isPreview() }">
    <br-manage-content-button :content="document" />

    <vsf-content
      :title="data.title"
      :author="data.author"
      :date="formatDate(date)"
      :content="page.rewriteLinks(data.content.value)"
    ></vsf-content>
  </div>
</template>

<script lang="ts">
import { ContainerItem, Document, ImageSet, Page, Reference } from '@bloomreach/spa-sdk';
import { BrManageContentButton } from '@bloomreach/vue-sdk';
import VsfContent from './VsfContent.vue';
import { PropType } from 'vue';
import { computed } from '@vue/composition-api';

interface DocumentContent {
  value: string;
}

interface DocumentData {
  author: string;
  content: DocumentContent;
  date: number;
  publicationDate: number;
  image: Reference;
  introduction: string;
  title: string;

  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  [property: string]: any;
}

export default {
  name: 'BrContent',
  components: {
    VsfContent,
    BrManageContentButton,
  },
  props: {
    page: {
      type: Object as PropType<() => Page>,
    },
    component: {
      type: Object as PropType<() => ContainerItem>,
    },
  },
  setup({ page }: { page: Page, component: ContainerItem }) {
    const document = computed(() => page.getDocument<Document>());
    const data = computed(() => document.value.getData<DocumentData>());
    const image = computed(() => data.value.image && page.getContent<ImageSet>(data.value.image));
    const date = computed(() => data.value.date ?? data.value.publicationDate);

    return {
      document,
      data,
      image,
      date,
    }
  },
  methods: {
    formatDate(date: number) {
      return new Date(date).toDateString();
    },
  },
};
</script>
