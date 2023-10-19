<script setup>
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    import {Head, Link} from '@inertiajs/vue3';
    import {toRefs, computed} from 'vue'

    import {useCartStore} from '@/store/cart'
    import {storeToRefs} from 'pinia';
    const cartStore = useCartStore()
    const {cart} = storeToRefs(cartStore)

    const removeFromCart = (id) => {
        cartStore.removeProductFromCart(id)
    }

    const total = computed(() => {
        let total = 0
        cart.value.forEach(c => {
            total += c.price
        })
        if (total > 0) {
            return total.toFixed(2)
        }
        return 0
    })

    const totalWithoutDot = () => {
        let num = String(total.value).split('.').join('')
        return Number(num)
    }
</script>

<template>

    <Head title="Checkout" />

    <AuthenticatedLayout>
        <div class="p-4 mt-2 max-w-[1250px] mx-auto text-3xl font-extrabold">Checkout</div>
        <div class="flex max-w-[1250px] mx-auto pt-4">
            <div class="w-8/12">
                <div class="flex items-stretch border-b border-b-gray-300 w-[calc(100%-100px)] pb-4 pl-4 mb-6">
                    <div class="text-gray-900 font-extrabold text-xl mr-12">
                        Shipping Address
                    </div>
                    <div class="px-4 font-semibold">
                        <div>{{$page.props.auth.user.first_name}} {{$page.props.auth.user.last_name}}</div>
                        <div>{{$page.props.auth.address.addr1}}</div>
                        <div>{{$page.props.auth.address.addr2}}</div>
                        <div>{{$page.props.auth.address.city}}</div>
                        <div>{{$page.props.auth.address.postcode}}</div>
                        <div>{{$page.props.auth.address.country}}</div>
                    </div>
                </div>
            </div>
            .
        </div>
    </AuthenticatedLayout>
</template>