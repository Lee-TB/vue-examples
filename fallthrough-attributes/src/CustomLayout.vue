<!-- Attribute Inheritance on Multiple Root Nodes -->
<!-- If <CustomLayout> has the following multi-root template, 
  there will be a warning because Vue cannot be sure 
  where to apply the fallthrough attributes -->
<template>
  <header></header>
  <!-- The warning will be suppressed if $attrs is explicitly bound -->
  <main v-bind="$attrs"></main>
  <footer></footer>
</template>
