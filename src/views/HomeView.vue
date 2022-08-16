<script lang="ts" setup>
import { ref, Ref } from "vue";

import QRCode from "qrcode";
import Swal from "sweetalert2";

const content: Ref<string> = ref("");

const generateQR = (): void => {
  const canvas: HTMLCanvasElement = document.getElementById(
    "canvas"
  ) as HTMLCanvasElement;

  if (content.value.trim() === "") {
    canvas.style.display = "none";
  } else {
    return QRCode.toCanvas(canvas, content.value, (err: any) => {
      if (err) {
        console.error(err);
        Swal.fire({
          toast: true,
          title: "Oops..!",
          text: err,
          icon: "error",
          position: "bottom",
        });
      }
      canvas.style.display = "block";
    });
  }
};
</script>

<template>
  <div class="home">
    <div class="h-screen grid place-items-center">
      <div class="p-6 border-4">
        <h1 class="font-bold text-3xl text-center mb-3">Miilkyy QR</h1>
        <em class="text-gray-500"
          >Miilkyy QR is a small and simple QR generator.</em
        >
        <div class="mb-3">
          <label class="block" for="content">Content</label>
          <input
            @keyup="generateQR"
            v-model="content"
            class="border-red-500 border-2 focus:outline-none p-1 w-full"
            name="content"
            id="content"
            type="text"
            placeholder="e.g. miilkyyQR"
          />
        </div>
        <canvas class="hidden" id="canvas"></canvas>
      </div>
    </div>
  </div>
</template>
