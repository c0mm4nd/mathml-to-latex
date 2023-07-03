<script setup>
import { NButton, NInput, NCard, NSpace } from 'naive-ui'
import * as Mathml2latex from 'mathml-to-latex'

import { reactive } from 'vue'

const state = reactive({
  input: `    <math>
        <mrow>
            <mi>A</mi>
            <mo>=</mo>
            <mfenced open = "[" close="]">
            <mtable>
                <mtr>
                <mtd><mi>x</mi></mtd>
                <mtd><mi>y</mi></mtd>
                </mtr>
                <mtr>
                <mtd><mi>z</mi></mtd>
                <mtd><mi>w</mi></mtd>
                </mtr>
            </mtable>
            </mfenced>
        </mrow>
    </math>`,
  output: String.raw`A = \begin{bmatrix} x & y \\ z & w \end{bmatrix}`,
})


const convert = () => {
  // console.log(input)
  state.output = Mathml2latex.convert(state.input) 
}

</script>

<template>
  <main>
    <h1 style="margin: 40px;"> MathML to Latex (online) </h1>

    <n-space justify="center">
      <n-card style="margin-top: 20px;">
        <n-input style="height: 60vh; width: 40vw;" v-model:value="state.input" type="textarea" placeholder="MathML Textarea" />
        <!-- {{ state.input }} -->
      </n-card>

      <n-card style="margin-top: 20px;">
        <n-input style="height: 60vh; width: 40vw;" v-model:value="state.output" type="textarea" placeholder="Latex Textarea" />
        <!-- {{ state.output }} -->
      </n-card>
    </n-space>
    <center style="margin-top: 20px;">
      <n-button @click="convert">Convert</n-button>
    </center>
  </main>
</template>

<style scoped></style>
