<template>
    <div class="products">
        <div class="image-container">
            <div style="overflow: hidden; width: 100%; height: 100%;">
                <img src="https://www.shutterstock.com/image-photo/fried-salmon-steak-cooked-green-600nw-2489026949.jpg"
                    alt="food-image">
            </div>
            <button class="overlay-button">
                <span class="material-symbols-outlined" style="color: #F25C05; margin-right: 1rem;">
                    add_shopping_cart
                </span>
                <p>Add to Cart</p>
            </button>
        </div>
        <div>
            <p style="font-weight: 200;">Pie</p>
            <p style="font-weight: 500; color: #25231b;">Lemon Menrigue Pie</p>
            <p style="font-weight: 600; color: #F25C05;">$4.00</p>
        </div>
    </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
.overlay-button {
    position: absolute;
    /* Posiciona o botão sobre a imagem */
    bottom: -15px;
    /* Metade do botão ficará fora da imagem */
    left: 50%;
    /* Centraliza horizontalmente */
    transform: translateX(-50%);
    /* Ajusta o alinhamento central */
    background-color: white;
    color: #25231b;
    border: 1px solid #F25C05;
    padding: 0.5rem 1rem;
    border-radius: 32px;
    cursor: pointer;
    z-index: 10;
    /* Garante que o botão fique acima da imagem */
    font-weight: 500;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    width: 60%;
}

.image-container {
    position: relative;
    /* Define o contêiner como referência para posicionamento absoluto */
    width: 100%;
    background-color: aquamarine;
    height: 70%;
}

.image-container img {
    height: 100%;
    width: 100%;
    object-fit: cover;
}

.products {
    flex: 1 1 220px;
    max-width: 260px;
    height: 360px;
    background-color: white;
    display: flex;
    flex-direction: column;
    overflow-y: auto;
    padding: 0.5rem;
    border-radius: 6px;
    justify-content: space-between;
}
</style>