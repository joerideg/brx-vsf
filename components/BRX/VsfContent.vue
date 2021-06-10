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
  <div>
    <img v-if="imageUrl" class="img-fluid mb-3" :src="imageUrl" :alt="title" />
    <h1 v-if="title">{{ title }}</h1>
    <p v-if="author" class="mb-3 text-muted">{{ author }}</p>
    <p v-if="date" class="mb-3 small text-muted">{{ date }}</p>
    <div v-if="content" v-html="content" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'VsfContent',
  props: {
    imageUrl: {
      type: String,
      default: '',
    },
    title: {
      type: String,
      default: '',
    },
    author: {
      type: String,
      default: '',
    },
    content: {
      type: String,
      default: '',
    },
    date: {
      type: String,
      default: '',
    },
  },
});
</script>
