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
    // Swal.fire({
    //   toast: true,
    //   title: 'Oops..!',
    //   text: 'Please fill the content field',
    //   icon: 'warning',
    //   position: 'bottom'
    // });
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
        <!-- <form> -->
        <div class="mb-3">
          <label class="block" for="content">Content</label>
          <input
            @keyup="generateQR"
            v-model="content"
            class="border-red-500 border-2 focus:outline-none p-1"
            name="content"
            id="content"
            type="text"
            placeholder="e.g. miilkyyQR"
          />
        </div>
        <!-- <div class="mb-3">
          <label class="block" for="size">Size</label>
          <select class="p-2 cursor-pointer" name="size" id="size">
            <option value="300x300">300x300</option>
          </select>
        </div> -->
        <!-- <button class="bg-red-500 text-white p-2 rounded" type="submit">Submit</button> -->
        <!-- </form> -->
        <canvas class="hidden" id="canvas"></canvas>
      </div>
    </div>
  </div>
</template>
