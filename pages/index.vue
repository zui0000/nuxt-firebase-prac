<template>
  <section class="container">
    <el-card style="flex: 1">
      <div slot="header" class="clearfix">
        <span>ログイン</span>
      </div>
      <!-- card body -->
      <form action="">
        <div class="form-content">
          <span>ユーザー</span>
          <el-input v-model="formData.id" placeholder="" />
        </div>
        <div class="form-content">
          <el-checkbox v-model="isCreateMode">アカウントを作成する</el-checkbox>
        </div>
        <div class="text-right">
          <el-button type="primary">
            {{ buttonText }}
          </el-button>
        </div>
      </form>
    </el-card>
  </section>
</template>
<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
@Component({
  // asyncData: async () => {
  //   return {
  //     isCreateMode: false,
  //     formData: {
  //       id: ''
  //     }
  //   }
  // }
})
export default class extends Vue {
  isCreateMode!: boolean
  formData = {
    id: ''
  }

  get buttonText() {
    return this.isCreateMode ? '新規登録' : 'ログイン'
  }
}
</script>
<style lang="sass">
.form-content
  margin: 16px 0
</style>
