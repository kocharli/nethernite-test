<script>
import { h } from 'vue';

const ErrorMessage = (props, context) => h(
  'small',
  {
    ...context.attrs,
    class: 'text-danger',
  },
  'Something is gone wrong',
);

export default ErrorMessage;
</script>
