<template>
  <div>
    <h1>Cifrado de Escítala</h1>
    <label for="mensaje">Texto a cifrar:</label><br />
    <textarea id="mensaje" rows="4" cols="50"></textarea><br />

    <button @click="cifrarMensaje()">Cifrar</button><br />
    <label for="resultado">Texto cifrado:</label><br />
    <textarea id="resultado" rows="4" cols="50"></textarea><br />

    <button @click="descifrarMensaje()">Descifrar Mensaje</button><br />
    <label for="resultado">Texto descifrado:</label><br />
    <textarea id="resultadod" rows="4" cols="50" readonly></textarea>
  </div>
</template>

<script setup lang="ts">
function cifrarMensaje(): void {
  const mensaje: string = (
    document.getElementById("mensaje") as HTMLTextAreaElement
  ).value;
  const columnas: number = parseInt(
    prompt("Ingrese el rango de cifrado:") || "0"
  );
  const mensajeCifrado: string = cifrarEscitala(mensaje, columnas);
  (document.getElementById("resultado") as HTMLTextAreaElement).value =
    mensajeCifrado;
}

function descifrarMensaje(): void {
  const mensajeCifrado: string = (
    document.getElementById("resultado") as HTMLTextAreaElement
  ).value;
  const columnas: number = parseInt(
    prompt("Ingrese el rango de cifrado:") || "0"
  );
  const mensajeDescifrado: string = descifrarEscitala(mensajeCifrado, columnas);
  (document.getElementById("resultadod") as HTMLTextAreaElement).value =
    mensajeDescifrado;
}

function cifrarEscitala(mensaje: string, columnas: number): string {
  const filas: number = Math.ceil(mensaje.length / columnas);
  const matriz: string[][] = Array(filas)
    .fill("")
    .map(() => Array(columnas).fill(""));

  let indice: number = 0;
  for (let i = 0; i < filas; i++) {
    for (let j = 0; j < columnas; j++) {
      if (indice < mensaje.length) {
        matriz[i][j] = mensaje.charAt(indice);
        indice++;
      }
    }
  }

  let mensajeCifrado: string = "";
  for (let i = 0; i < columnas; i++) {
    for (let j = 0; j < filas; j++) {
      mensajeCifrado += matriz[j][i];
    }
  }

  return mensajeCifrado;
}

function descifrarEscitala(mensajeCifrado: string, columnas: number): string {
  const filas: number = Math.ceil(mensajeCifrado.length / columnas);
  const matriz: string[][] = Array(filas)
    .fill("")
    .map(() => Array(columnas).fill(""));

  let indice: number = 0;
  for (let i = 0; i < columnas; i++) {
    for (let j = 0; j < filas; j++) {
      if (indice < mensajeCifrado.length) {
        matriz[j][i] = mensajeCifrado.charAt(indice);
        indice++;
      }
    }
  }

  let mensajeDescifrado: string = "";
  for (let i = 0; i < filas; i++) {
    for (let j = 0; j < columnas; j++) {
      mensajeDescifrado += matriz[i][j];
    }
  }

  return mensajeDescifrado;
}
</script>

<style scoped>

</style>
