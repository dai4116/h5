<template>
    <div
    class="modal fade show"
    id="myModal"
    tabindex="-1"
    role="dialog"
    aria-labelledby="myModalTitle"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered" role="document">
      <div class="modal-content">
        <div class="modal-header d-flex justify-content-center">
          <div class="modal-title-bg">
            <div class="modal-title text-center" id="myModalTitle">
              提示
            </div>
          </div>

          <div
            type="button"
            class="modal-close"
            data-dismiss="modal"
            aria-label="Close"
          >
            <span aria-hidden="true">&times;</span>
          </div>
        </div>
        <div class="modal-body text-center">
          帳號或密碼輸入錯誤
        </div>
        <div class="modal-footer d-flex justify-content-center">
          <div class="l-btn submit-active-btn" data-dismiss="modal">確定</div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
