<template>
  <div>
    <ft-loader
      v-if="isLoading"
    />
    <div
      v-if="!isLoading && errorChannels.length !== 0"
    >
      <h3> {{ $t("Subscriptions.Error Channels") }}</h3>
      <ft-flex-box>
        <ft-channel-bubble
          v-for="(channel, index) in errorChannels"
          :key="index"
          :channel-name="channel.name"
          :channel-id="channel.id"
          :channel-thumbnail="channel.thumbnail"
        />
      </ft-flex-box>
    </div>
    <ft-flex-box
      v-if="!isLoading && activeVideoList.length === 0"
    >
      <p
        v-if="activeSubscriptionList.length === 0"
        class="message"
      >
        {{ $t("Subscriptions['Your Subscription list is currently empty. Start adding subscriptions to see them here.']") }}
      </p>
      <p
        v-else-if="!fetchSubscriptionsAutomatically && !attemptedFetch"
        class="message"
      >
        {{ $t("Subscriptions.Disabled Automatic Fetching") }}
      </p>
      <p
        v-else
        class="message"
      >
        {{ $t("Subscriptions.Empty Channels") }}
      </p>
    </ft-flex-box>
    <ft-element-list
      v-if="!isLoading && activeVideoList.length > 0"
      :data="activeVideoList"
      :use-channels-hidden-preference="false"
    />
    <ft-flex-box
      v-if="!isLoading && videoList.length > dataLimit"
    >
      <ft-button
        :label="$t('Subscriptions.Load More Videos')"
        background-color="var(--primary-color)"
        text-color="var(--text-with-main-color)"
        @click="increaseLimit"
      />
    </ft-flex-box>
    <ft-icon-button
      v-if="!isLoading"
      :icon="['fas', 'sync']"
      class="floatingTopButton"
      :title="$t('Subscriptions.Refresh Subscriptions')"
      :size="12"
      theme="primary"
      @click="$emit('refresh')"
    />
  </div>
</template>

<script src="./subscriptions-tab-ui.js" />
<style scoped src="./subscriptions-tab-ui.css" />
