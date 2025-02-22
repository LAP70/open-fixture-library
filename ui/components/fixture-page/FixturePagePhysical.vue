<template>
  <div class="physical">

    <section>
      <LabeledValue
        v-if="physical.dimensions !== null"
        name="dimensions"
        label="Dimensions">
        {{ physical.width }} &times;
        {{ physical.height }} &times;
        {{ physical.depth }}mm
        <span class="hint">width &times; height &times; depth</span>
      </LabeledValue>

      <LabeledValue
        v-if="physical.weight !== null"
        name="weight"
        label="Weight">
        {{ physical.weight }}kg
      </LabeledValue>

      <LabeledValue
        v-if="physical.power !== null"
        name="power"
        label="Power">
        {{ physical.power }}W
      </LabeledValue>

      <LabeledValue
        v-if="physical.DMXconnector !== null"
        name="DMXconnector"
        label="DMX connector">
        {{ physical.DMXconnector }}
      </LabeledValue>
    </section>

    <section v-if="physical.hasBulb" class="bulb">
      <h4>Bulb</h4>

      <LabeledValue
        v-if="physical.bulbType !== null"
        name="bulb-type"
        label="Bulb type">
        {{ physical.bulbType }}
      </LabeledValue>

      <LabeledValue
        v-if="physical.bulbColorTemperature !== null"
        name="bulb-colorTemperature"
        label="Color temperature">
        {{ physical.bulbColorTemperature }}K
      </LabeledValue>

      <LabeledValue
        v-if="physical.bulbLumens !== null"
        name="bulb-lumens"
        label="Lumens">
        {{ physical.bulbLumens }}lm
      </LabeledValue>
    </section>

    <section v-if="physical.hasLens" class="lens">
      <h4>Lens</h4>

      <LabeledValue
        v-if="physical.lensName !== null"
        name="lens-name"
        label="Name">
        {{ physical.lensName }}
      </LabeledValue>

      <LabeledValue
        v-if="physical.lensDegreesMin !== null"
        name="lens-degreesMinMax"
        label="Beam angle">
        {{ physical.lensDegreesMin === physical.lensDegreesMax
          ? `${physical.lensDegreesMin}°`
          : `${physical.lensDegreesMin}…${physical.lensDegreesMax}°`
        }}
      </LabeledValue>
    </section>

    <section v-if="physical.hasMatrixPixels" class="matrixPixels">
      <h4>Matrix Pixels</h4>

      <LabeledValue
        v-if="physical.matrixPixelsDimensions !== null"
        name="dimensions"
        label="Pixel dimensions">
        {{ physical.matrixPixelsDimensions[0] }} &times;
        {{ physical.matrixPixelsDimensions[1] }} &times;
        {{ physical.matrixPixelsDimensions[2] }}mm
        <span class="hint">width &times; height &times; depth</span>
      </LabeledValue>

      <LabeledValue
        v-if="physical.matrixPixelsSpacing !== null"
        name="dimensions"
        label="Pixel spacing">
        {{ physical.matrixPixelsSpacing[0] }} &times;
        {{ physical.matrixPixelsSpacing[1] }} &times;
        {{ physical.matrixPixelsSpacing[2] }}mm
        <span class="hint">left/right &times; top/bottom &times; ahead/aback</span>
      </LabeledValue>
    </section>

  </div>
</template>

<style lang="scss" scoped>
.physical {
  columns: 2 350px;
  column-gap: 3rem;

  & > section {
    padding: 0 0 1.2ex;
    overflow: hidden;
    break-inside: avoid;

    &:empty {
      display: none;
    }
  }

  h4 {
    margin: 0;
  }
}
</style>

<script>
import { instanceOfProp } from 'vue-ts-types';
import Physical from '../../../lib/model/Physical.js';

import LabeledValue from '../LabeledValue.vue';

export default {
  components: {
    LabeledValue,
  },
  props: {
    physical: instanceOfProp(Physical).required,
  },
};
</script>
