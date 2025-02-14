<template>
    <div class="bg-white">
      <header>
        <nav class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8" aria-label="Global">
          <a href="#" class="-m-1.5 p-1.5">
            <span class="sr-only">Your Company</span>
            <img class="h-8 w-auto" src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Emblem_of_Maldives.svg/240px-Emblem_of_Maldives.svg.png" alt="" />
          </a>
          <div class="flex lg:hidden">
            <button type="button" class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700" @click="mobileMenuOpen = true">
              <span class="sr-only">Open main menu</span>
                <svg class="size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                </svg>
            </button>
          </div>
          <div class="hidden lg:flex lg:gap-x-12">
            <a v-for="item in navigation" :key="item.name" :href="item.href" class="text-sm/6 font-semibold text-gray-900">{{ item.name }}</a>
            <a href="#" class="text-sm/6 font-semibold text-gray-900">Log in <span aria-hidden="true">&rarr;</span></a>
          </div>
        </nav>
        <Dialog class="lg:hidden" @close="mobileMenuOpen = false" :open="mobileMenuOpen">
          <div class="fixed inset-0 z-50" />
          <DialogPanel class="fixed inset-y-0 right-0 z-50 w-full overflow-y-auto bg-white px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10">
            <div class="flex items-center justify-between">
              <a href="#" class="-m-1.5 p-1.5">
                <span class="sr-only">Your Company</span>
                <img class="h-8 w-auto" src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Emblem_of_Maldives.svg/240px-Emblem_of_Maldives.svg.png" alt="" />
              </a>
              <button type="button" class="-m-2.5 rounded-md p-2.5 text-gray-700" @click="mobileMenuOpen = false">
                <span class="sr-only">Close menu</span>
                <svg class="size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
                </svg>
              </button>
            </div>
            <div class="mt-6 flow-root">
              <div class="-my-6 divide-y divide-gray-500/10">
                <div class="space-y-2 py-6">
                  <a v-for="item in navigation" :key="item.name" :href="item.href" class="-mx-3 block rounded-lg px-3 py-2 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">{{ item.name }}</a>
                </div>
                <div class="py-6">
                  <a href="#" class="-mx-3 block rounded-lg px-3 py-2.5 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">Log in</a>
                </div>
              </div>
            </div>
          </DialogPanel>
        </Dialog>
      </header>
  
      <main>
        <!-- Pricing section -->
        <div class="mx-auto mt-16 max-w-7xl px-6 sm:mt-32 lg:px-8">
          <div class="mx-auto max-w-4xl text-center">
            <h1 class="text-base/7 font-semibold text-indigo-600">Pricing</h1>
            <p class="mt-2 text-balance text-5xl font-semibold tracking-tight text-gray-900 sm:text-6xl">Pricing that grows with you</p>
          </div>
          <p class="mx-auto mt-6 max-w-2xl text-pretty text-center text-lg font-medium text-gray-600 sm:text-xl/8">Choose an affordable plan that’s packed with the best features for engaging your audience, creating customer loyalty, and driving sales.</p>
          <div class="mt-16 flex justify-center">
            <fieldset aria-label="Payment frequency">
              <RadioGroup v-model="frequency" class="grid grid-cols-2 gap-x-1 rounded-full p-1 text-center text-xs/5 font-semibold ring-1 ring-inset ring-gray-200">
                <RadioGroupOption as="template" v-for="option in pricing.frequencies" :key="option.value" :value="option" v-slot="{ checked }">
                  <div :class="[checked ? 'bg-indigo-600 text-white' : 'text-gray-500', 'cursor-pointer rounded-full px-2.5 py-1']">{{ option.label }}</div>
                </RadioGroupOption>
              </RadioGroup>
            </fieldset>
          </div>
          <div class="isolate mx-auto mt-10 grid max-w-md grid-cols-1 gap-8 md:max-w-2xl md:grid-cols-1 lg:max-w-4xl xl:mx-0 xl:max-w-none xl:grid-cols-2">
            <div v-for="tier in pricing.tiers" :key="tier.id" :class="[tier.mostPopular ? 'ring-2 ring-indigo-600' : 'ring-1 ring-gray-200', 'rounded-3xl p-8']">
              <h2 :id="tier.id" :class="[tier.mostPopular ? 'text-indigo-600' : 'text-gray-900', 'text-lg/8 font-semibold']">{{ tier.name }}</h2>
              <p class="mt-4 text-sm/6 text-gray-600">{{ tier.description }}</p>
              <p class="mt-6 flex items-baseline gap-x-1">
                <span class="text-4xl font-semibold tracking-tight text-gray-900">{{ tier.price[frequency.value] }}</span>
                <span class="text-sm/6 font-semibold text-gray-600">{{ frequency.priceSuffix }}</span>
              </p>
              <a :href="tier.href" :aria-describedby="tier.id" :class="[tier.mostPopular ? 'bg-indigo-600 text-white shadow-sm hover:bg-indigo-500' : 'text-indigo-600 ring-1 ring-inset ring-indigo-200 hover:ring-indigo-300', 'mt-6 block rounded-md px-3 py-2 text-center text-sm/6 font-semibold focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600']">Buy plan</a>
              <ul role="list" class="mt-8 space-y-3 text-sm/6 text-gray-600">
                <li v-for="feature in tier.features" :key="feature" class="flex gap-x-3">
                  <!-- <CheckIcon class="h-6 w-5 flex-none text-indigo-600" aria-hidden="true" /> -->
                  {{ feature }}
                </li>
              </ul>
            </div>
          </div>
        </div>
  
        
  
        <!-- FAQ section -->
        <div class="mx-auto my-24 max-w-7xl px-6 sm:my-56 lg:px-8">
          <div class="mx-auto max-w-4xl">
            <h2 class="text-4xl font-semibold tracking-tight text-gray-900 sm:text-5xl">Frequently asked questions</h2>
            <dl class="mt-16 divide-y divide-gray-900/10">
              <Disclosure as="div" v-for="faq in faqs" :key="faq.question" class="py-6 first:pt-0 last:pb-0" v-slot="{ open }">
                <dt>
                  <DisclosureButton class="flex w-full items-start justify-between text-left text-gray-900">
                    <span class="text-base/7 font-semibold">{{ faq.question }}</span>
                    <span class="ml-6 flex h-7 items-center">
                        <svg v-if="!open" class="size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v12m6-6H6" />
                        </svg>
                        <svg v-else class="size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M18 12H6" />
                        </svg>
                    </span>
                  </DisclosureButton>
                </dt>
                <DisclosurePanel as="dd" class="mt-2 pr-12">
                  <p class="text-base/7 text-gray-600">{{ faq.answer }}</p>
                </DisclosurePanel>
              </Disclosure>
            </dl>
          </div>
        </div>
      </main>
  
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import {
    Dialog,
    DialogPanel,
    Disclosure,
    DisclosureButton,
    DisclosurePanel,
    RadioGroup,
    RadioGroupOption,
  } from '@headlessui/vue'
  
  const navigation = [
    { name: 'Product', href: route('dashboard') },
    { name: 'Features', href: '#' },
    { name: 'Marketplace', href: '#' },
    { name: 'Company', href: '#' },
  ]
  const pricing = {
    frequencies: [
      { value: 'monthly', label: 'Monthly', priceSuffix: '/month' },
      { value: 'annually', label: 'Annually', priceSuffix: '/year' },
    ],
    tiers: [
      {
        name: 'Hobby',
        id: 'tier-hobby',
        href: '#',
        price: { monthly: '$19', annually: '$199' },
        description: 'The essentials to provide your best work for clients.',
        features: ['5 products', 'Up to 1,000 subscribers', 'Basic analytics'],
        mostPopular: false,
      },
      {
        name: 'Freelancer',
        id: 'tier-freelancer',
        href: '#',
        price: { monthly: '$29', annually: '$299' },
        description: 'The essentials to provide your best work for clients.',
        features: ['5 products', 'Up to 1,000 subscribers', 'Basic analytics', '48-hour support response time'],
        mostPopular: false,
      },
      {
        name: 'Startup',
        id: 'tier-startup',
        href: '#',
        price: { monthly: '$59', annually: '$599' },
        description: 'A plan that scales with your rapidly growing business.',
        features: [
          '25 products',
          'Up to 10,000 subscribers',
          'Advanced analytics',
          '24-hour support response time',
          'Marketing automations',
        ],
        mostPopular: true,
      },
      {
        name: 'Enterprise',
        id: 'tier-enterprise',
        href: '#',
        price: { monthly: '$99', annually: '$999' },
        description: 'Dedicated support and infrastructure for your company.',
        features: [
          'Unlimited products',
          'Unlimited subscribers',
          'Advanced analytics',
          '1-hour, dedicated support response time',
          'Marketing automations',
          'Custom reporting tools',
        ],
        mostPopular: false,
      },
    ],
  }
  const faqs = [
    {
      question: "What's the best thing about Switzerland?",
      answer:
        "I don't know, but the flag is a big plus. Lorem ipsum dolor sit amet consectetur adipisicing elit. Quas cupiditate laboriosam fugiat.",
    },
    // More questions...
  ]
  
  const mobileMenuOpen = ref(false)
  const frequency = ref(pricing.frequencies[0])
  </script>