<template>
<h1>No Access to this page</h1>
</template>
<script>
export default {
  name: 'NoAccess',
  mounted(){
    window.location.href = "https://cloudcobus.auth.eu-west-1.amazoncognito.com/login?client_id=6uad7uthfhv3a7p9aihdbjl3tt&response_type=token&scope=aws.cognito.signin.user.admin+email+openid+phone+profile&redirect_uri=http://localhost:5173"
  }
}
</script>
<style>
</style>