<template>
  <div>
    <p>{{ defaultText }}</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  computed: {
    defaultText() {
      return browser.i18n.getMessage('extName');
    },
  },
  mounted() {
    browser.runtime.sendMessage({});
  },
};
</script>

<style lang="scss" scoped>
p {
  font-size: 20px;
  text-align: center;
}
</style>
