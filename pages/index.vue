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
          <el-button type="primary" @click="handleClickSubmit">
            {{ buttonText }}
          </el-button>
        </div>
      </form>
    </el-card>
  </section>
</template>
<script lang="ts">
import { Context } from '@nuxt/types'
import { Component, Vue } from 'nuxt-property-decorator'
// import { mapActions, mapGetters } from 'vuex'
import Cookies from 'universal-cookie'
@Component({})
export default class extends Vue {
  isCreateMode!: boolean
  formData!: any
  user!: string

  asyncData(context: Context) {
    if (context.store.getters.user) context.redirect('/posts/')
    return {
      isCreateMode: false,
      formData: {
        id: ''
      }
    }
  }

  get buttonText(): string {
    return this.isCreateMode ? '新規登録' : 'ログイン'
  }

  async handleClickSubmit() {
    const cookies = new Cookies()
    if (this.isCreateMode) {
      try {
        await this.$store.dispatch('register', { ...this.formData })
        this.$notify({
          type: 'success',
          title: 'アカウント作成完了',
          message: `${this.formData.id} として登録しました。`,
          position: 'bottom-right',
          duration: 1000
        })
        cookies.set('user', JSON.stringify(this.user))
        this.$router.push('/posts/')
      } catch (e) {
        this.$notify({
          title: 'アカウント作成失敗',
          message: `既に登録されているユーザーか、不正なユーザーです。`,
          position: 'bottom-right',
          duration: 1000
        })
      }
    } else {
      try {
        await this.$store.dispatch('login', { ...this.formData })
        this.$notify({
          type: 'success',
          title: 'ログイン成功。',
          message: `${this.formData.id} としてログインしました。`,
          position: 'bottom-right',
          duration: 1000
        })
        cookies.set('user', JSON.stringify(this.user))
        this.$router.push('/posts/')
      } catch (e) {
        this.$notify({
          title: 'ログイン失敗',
          message: `不正なユーザーID です。`,
          position: 'bottom-right',
          duration: 1000
        })
      }
    }
  }
}
</script>
<style lang="sass">
.form-content
  margin: 16px 0
</style>
