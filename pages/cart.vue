<template>
      <div class="h-full bg-gray-100 py-20">
            <!-- heading -->
            <h1 class="mb-10 text-center text-2xl font-bold">Cart Items</h1>
            <div class="mx-auto max-w-5xl justify-center px-6 md:flex md:space-x-6 xl:px-0">
                  <!-- cart product list container-->
                  <div class="rounded-lg md:w-2/3">
                        <!-- cart product -->
                        <div v-if="cartItems.cartItems.length" v-for="item, i in cartItems.cartItems" :key="i"
                              class="justify-between mb-6 rounded-lg bg-white p-6 shadow-md sm:flex sm:justify-start">
                              <!-- product img -->
                              <img :src="item.thumbnail" alt="product-image"
                                    class="w-full h-32 rounded-lg sm:w-40 object-contain" />
                              <!-- END -->
                              <div class="sm:ml-4 sm:flex sm:w-full sm:justify-between">
                                    <div class="mt-5 sm:mt-0">
                                          <h2 class="text-lg font-bold text-gray-900">{{ item.title }}</h2>
                                          <p class="mt-1 text-xs text-gray-700">{{ item.category }}</p>
                                    </div>
                                    <!-- Quantity , remove and price -->
                                    <div class="mt-4 sm:space-y-6 sm:mt-0 sm:block sm:space-x-6">
                                          <div class=" border-gray-100">
                                                <span @click="cartItems.subQnt(i)"
                                                      class="cursor-pointer rounded-l bg-gray-100 py-1 px-3.5 duration-100 hover:bg-blue-500 hover:text-blue-50">
                                                      - </span>
                                                <input class="h-8 w-8 border bg-white text-center text-xs outline-none"
                                                      type="number" :value="item.quantity" min="1" />
                                                <span @click="cartItems.addQnt(i)"
                                                      class="cursor-pointer rounded-r bg-gray-100 py-1 px-3 duration-100 hover:bg-blue-500 hover:text-blue-50">
                                                      + </span>
                                          </div>
                                          <div>
                                                <p class="text-sm font-bold">$ {{ item.price }} </p>
                                                <button @click="cartItems.removeCartItem(i)"
                                                      class="mt-6 w-full rounded-md bg-blue-500 py-1.5 font-medium text-blue-50 hover:bg-blue-600">
                                                      Remove
                                                </button>
                                          </div>
                                    </div>
                                    <!-- END -->
                              </div>
                        </div>

                        <!-- when cart is empty -->
                        <!-- <div v-else
                              class="flex flex-col w-full gap-5 p-2 mx-auto bg-white shadow-lg select-none sm:p-4 sm:h-64 rounded-2xl sm:flex-row ">
                              <div class="bg-gray-200 h-52 sm:h-full sm:w-72 rounded-xl animate-pulse">
                              </div>
                              <div class="flex flex-col flex-1 gap-5 sm:p-2">
                                    <div class="flex flex-col flex-1 gap-3">
                                          <div class="w-full bg-gray-200 animate-pulse h-14 rounded-2xl">
                                          </div>
                                          <div class="w-full h-3 bg-gray-200 animate-pulse rounded-2xl">
                                          </div>
                                          <div class="w-full h-3 bg-gray-200 animate-pulse rounded-2xl">
                                          </div>
                                          <div class="w-full h-3 bg-gray-200 animate-pulse rounded-2xl">
                                          </div>
                                          <div class="w-full h-3 bg-gray-200 animate-pulse rounded-2xl">
                                          </div>
                                    </div>
                                    <div class="flex gap-3 mt-auto">
                                          <div class="w-20 h-8 bg-gray-200 rounded-full animate-pulse">
                                          </div>
                                          <div class="w-20 h-8 bg-gray-200 rounded-full animate-pulse">
                                          </div>
                                          <div class="w-20 h-8 ml-auto bg-gray-200 rounded-full animate-pulse">
                                          </div>
                                    </div>
                              </div>
                        </div> -->

                        <EmptyCart v-else />
                  </div>
                  <!-- Sub total -->
                  <div class="bg-fixed mt-6 h-full rounded-lg border bg-white p-6 pb-10 shadow-md md:mt-0 md:w-1/3">
                        <div class="mb-2 flex justify-between">
                              <p class="text-gray-700">Subtotal</p>
                              <p class="text-gray-700">${{ subtotal }}</p>
                        </div>
                        <div class="flex justify-between">
                              <p class="text-gray-700">Shipping</p>
                              <p class="text-gray-700">${{ shipping }}</p>
                        </div>
                        <hr class="my-4" />
                        <div class="flex justify-between">
                              <p class="text-lg font-bold">Total</p>
                              <div class="">
                                    <p class="mb-1 text-lg font-bold">${{ (subtotal + shipping).toFixed(2) }} USD</p>
                                    <p class="text-sm text-gray-700">including VAT</p>
                              </div>
                        </div>
                        <button
                              class="mt-6 w-full rounded-md bg-blue-500 py-1.5 font-medium text-blue-50 hover:bg-blue-600">Check
                              out
                        </button>
                        <button type="button"
                              class="bg-blue-400 fixed bottom-16 rounded-full grid place-items-center transition-all duration-300 right-[20px] z-90 w-[48px] h-[48px]"></button>
                  </div>
            </div>
      </div>
</template>

<script setup lang="ts">
import { useCartStore } from '~/store/cartStore';


const cartItems = useCartStore()
const shipping = computed(() => +(cartItems.totalPrice / 16).toFixed(2))
const subtotal = computed(() => +(cartItems.totalPrice).toFixed(2))

</script>