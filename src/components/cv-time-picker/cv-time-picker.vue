<template>
  <div class="cv-time-picker bx--form-item">
    <div
      class="bx--time-picker"
      :class="{ 'bx--time-picker--light': theme === 'light' }"
    >
      <div class="bx--time-picker__input">
        <input
          :id="uid"
          type="text"
          class="bx--time-picker__input-field"
          :pattern="pattern"
          v-bind="$attrs"
          :placeholder="placeholder"
          :maxlength="placeholder.length"
          :data-invalid="invalidMessage.length > 0"
          :value="time"
          :disabled="disabled"
          @input="$emit('update:time', $event.target.value)"
        />
        <div class="bx--form-requirement" v-if="invalidMessage.length > 0">
          {{ invalidMessage }}
        </div>
        <label :for="uid" class="bx--label">{{ label }}</label>
      </div>
      <cv-select
        class="bx--time-picker__select"
        inline
        :form-item="false"
        hide-label
        :label="ampmSelectLabel"
        @input="$emit('update:ampm', $event)"
        :value="ampm"
        :disabled="disabled"
      >
        <cv-select-option class="bx--select-option" value="AM"
          >AM</cv-select-option
        >
        <cv-select-option class="bx--select-option" value="PM"
          >PM</cv-select-option
        >
      </cv-select>

      <cv-select
        class="bx--time-picker__select"
        inline
        :form-item="false"
        hide-label
        :label="timezonesSelectLabel"
        v-if="timezones.length > 0"
        :value="validTimezone"
        @input="$emit('update:timezone', $event)"
        :disabled="disabled"
      >
        <cv-select-option
          class="bx--select-option"
          v-for="item in timezones"
          :key="item.value"
          :value="item.value"
          >{{ item.label }}</cv-select-option
        >
      </cv-select>
    </div>
  </div>
</template>

<script>
import uidMixin from '../../mixins/uid-mixin';
import themeMixin from '../../mixins/theme-mixin';

export default {
  name: 'CvTimePicker',
  mixins: [uidMixin, themeMixin],
  inheritAttrs: false,
  props: {
    ampm: {
      type: String,
      default: 'AM',
    },
    ampmSelectLabel: { type: String, default: 'Select AM/PM' },
    disabled: Boolean,
    invalidMessage: { type: String, default: '' },
    label: { type: String, default: 'Select a time' },
    pattern: { type: String, default: '([01][0-9]:[0-6][0-9])' },
    placeholder: { type: String, default: 'hh:mm' },
    time: String,
    timezone: String,
    timezones: { type: Array, default: () => [] },
    timezonesSelectLabel: { type: String, default: 'Select time zone' },
  },
  computed: {
    validAmpm() {
      let result = this.ampm;
      if (!['AM', 'PM'].includes(this.ampm)) {
        console.error(
          `CvTimePicker: invalid value '${
            this.ampm
          }' supplied for prop ampm. Default applied.`
        );
        // set to valid value
        result = this.ampm[0].value;
        this.$emit('update:ampm', result);
      }
      return result;
    },
    validTimezone() {
      // Validate timezone setting
      let result = this.timezone;
      if (this.timezones && this.timezones.length) {
        if (!this.timezones.find(item => item.value === this.timezone)) {
          console.error(
            `CvTimePicker: invalid value '${
              this.timezone
            }' supplied for prop timezone. Default applied.`
          );
          // set to first valid value
          result = this.timezones[0].value;
          this.$emit('update:timezone', result);
        }
      }
      return result;
    },
  },
};
</script>

<style lang="scss"></style>
