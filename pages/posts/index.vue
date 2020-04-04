<template>
  <section class="container posts-page">
    <el-card>
      <div slot="header" class="clearfix">
        <span>
          新規登録
        </span>
      </div>
      <el-table :data="showPosts" style="width: 100%;" class="table">
        <el-table-colume prop="title" label="タイトル" />
        <el-table-colume prop="user.id" label="投稿者" width="180" />
        <el-table-colume props="created_at" label="投稿日時" width="240" />
      </el-table>
    </el-card>
  </section>
</template>
<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
@Component({})
export default class extends Vue {
  get showPosts() {
    return [
      {
        id: '001',
        title: 'How to development Nuxt.js Application',
        body: 'Learn ipsum dolor sit amet, hogehoge',
        created_at: '2020/04/01 12:00:00',
        user: {
          id: 'potato4'
        }
      },
      {
        id: '002',
        title: 'Development Nuxt.js Application to Heroku',
        body: 'Learn ipsum dolor sit amet, hogehoge',
        created_at: '2020/04/01 12:00:00',
        user: {
          id: 'potato4'
        }
      }
    ]
  }
}
</script>
<style lang="sass" scoped>
.post-page .eltable__row
  cursor: pointer
</style>
