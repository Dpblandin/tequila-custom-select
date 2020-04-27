<template>
  <div>
    <select :disabled="$attrs.disabled" ref="select" class="form-control" @change="change">
      <slot v-if="placeholderOption">
        <option value="">{{ placeholderOption }}</option>
      </slot>
      <option v-for="(option, index) in options"
              :key="index" :value="option[optionValueKey]"
              :selected="selectedOption(option[optionValueKey])">
        {{ option[optionLabelKey] }}
      </option>
    </select>
  </div>
</template>

<script>
  import customSelect from 'custom-select';

  const defaultOptionKeys = () => (['value', 'label']);

  export default {
    name: 'teq-custom-select',
    props: {
      options: {
        required: true,
      },
      selectedValue: {
        required: false,
      },
      optionKeys: {
        required: false,
        default: defaultOptionKeys,
      },
      customSelectOptions: {
        required: false,
        default: () => ({})
      },
      placeholderOption: {
        required: false,
        default: null,
      },
    },
    data: () => ({
      selected: null,
      customSelects: null,
    }),
    computed: {
      optionValueKey() {
        return this.optionKeys[0];
      },
      optionLabelKey() {
        return this.optionKeys[1];
      }
    },
    watch: {
      selectedValue(newValue, oldValue) {
        if (newValue === oldValue) {
          return;
        }
        this.customSelects[0].value = newValue;
      }
    },
    mounted() {
      this.customSelects = customSelect(this.$refs.select, this.customSelectOptions);
      this.$emit('custom-select-ready', this.customSelects);
    },
    methods: {
      selectedOption(optionValue) {
        return optionValue === this.selectedValue;
      },
      change(e) {
        const value = e.target.value;
        const option = this.options.find(option => value === option[this.optionValueKey]);
        this.$emit('input', {
          name: this.$refs.select.getAttribute('name'),
          value: option ? option[this.optionValueKey] : value,
        });
      }
    }
  }
</script>
