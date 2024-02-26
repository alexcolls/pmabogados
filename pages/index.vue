<template>
  <div>
    <ULandingHero
      :title="content.hero.title"
      :description="content.hero.description"
      :links="content.hero.links"
    >
      <template #headline>
        <UBadge
          v-if="content.hero.headline"
          variant="subtle"
          size="lg"
          class="relative rounded-full font-semibold"
        >
          <NuxtLink
            :to="content.hero.headline.to"
            target="_blank"
            class="focus:outline-none"
            tabindex="-1"
          >
            <span class="absolute inset-0" aria-hidden="true" />
          </NuxtLink>

          {{ content.hero.headline.label }}

          <UIcon
            v-if="content.hero.headline.icon"
            :name="content.hero.headline.icon"
            class="ml-1 w-4 h-4 pointer-events-none"
          />
        </UBadge>
      </template>

      <div>
        <video loop muted playsinline class="w-full h-auto">
          <source src="assets/vid/video.mp4" type="video/mp4">
        </video>
      </div>

      <ULandingLogos :title="content.logos.title" align="center">
        <UIcon
          v-for="icon in content.logos.icons"
          :key="icon"
          :name="icon"
          class="w-12 h-12 lg:w-16 lg:h-16 flex-shrink-0 text-gray-900
            dark:text-white"
        />
      </ULandingLogos>
    </ULandingHero>

    <ULandingSection
      :title="content.features.title"
      :description="content.features.description"
      :headline="content.features.headline"
    >
      <UPageGrid
        id="features"
        class="scroll-mt-[calc(var(--header-height)+140px+128px+96px)]"
      >
        <ULandingCard
          v-for="(item, index) in content.features.items"
          :key="index"
          v-bind="item"
        />
      </UPageGrid>
    </ULandingSection>

    <ULandingSection
      :title="content.pricing.title"
      :description="content.pricing.description"
      :headline="content.pricing.headline"
    >
      <UPricingGrid
        id="pricing"
        compact
        class="scroll-mt-[calc(var(--header-height)+140px+128px+96px)]"
      >
        <UPricingCard
          v-for="(plan, index) in content.pricing.plans"
          :key="index"
          v-bind="plan"
        />
      </UPricingGrid>
    </ULandingSection>

    <ULandingSection
      :headline="content.testimonials.headline"
      :title="content.testimonials.title"
      :description="content.testimonials.description"
    >
      <UPageColumns
        id="testimonials"
        class="xl:columns-4
          scroll-mt-[calc(var(--header-height)+140px+128px+96px)]"
      >
        <div
          v-for="(testimonial, index) in content.testimonials.items"
          :key="index"
          class="break-inside-avoid"
        >
          <ULandingTestimonial v-bind="testimonial" />
        </div>
      </UPageColumns>
    </ULandingSection>

    <ULandingSection
      class="bg-primary-50 dark:bg-primary-400 dark:bg-opacity-10"
    >
      <ULandingCTA v-bind="content.cta" :card="false" />
    </ULandingSection>

    <ULandingSection
      id="faq"
      :title="content.faq.title"
      :description="content.faq.description"
      class="scroll-mt-[var(--header-height)]"
    >
      <ULandingFAQ
        multiple
        :items="content.faq.items"
        :ui="{
          button: {
            label: 'font-semibold',
            trailingIcon: {
              base: 'w-6 h-6'
            }
          }
        }"
        class="max-w-4xl mx-auto"
      />
    </ULandingSection>
  </div>
</template>

<script setup lang="ts">

const { data: content } = await useAsyncData(
  'index', () => queryContent('/').findOne()
);

useSeoMeta({
  title: content.value.title,
  ogTitle: content.value.title,
  description: content.value.description,
  ogDescription: content.value.description
});

</script>
