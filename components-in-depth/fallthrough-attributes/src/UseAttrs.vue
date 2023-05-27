<!-- If needed, you can access a component's fallthrough attributes 
  in <script setup> using the useAttrs() API -->
<script setup>
import { useAttrs } from 'vue';

const attrs = useAttrs();
console.log(attrs);
</script>
