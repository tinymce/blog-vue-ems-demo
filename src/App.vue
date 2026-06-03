<script setup lang="ts">
import { ref } from 'vue'

const email = ref({
  from: '',
  to: '',
  subject: '',
  content: ''
})

const selectedSegment = ref<string | null>(null)
const sendTime = ref('now')

const segments = [
  { id: 'all', name: 'All Subscribers', count: 12543 },
  { id: 'active', name: 'Active Users', count: 8234 },
  { id: 'inactive', name: 'Inactive (30d+)', count: 4309 },
  { id: 'premium', name: 'Premium Members', count: 1876 }
]

const stats = {
  totalSubscribers: 12543,
  openRate: 28.4,
  clickRate: 3.2,
  unsubscribeRate: 0.8
}

const resetForm = () => {
  email.value = {
    from: '',
    to: '',
    subject: '',
    content: ''
  }
}

const selectSegment = (segmentId: string) => {
  selectedSegment.value = segmentId
}
</script>

<template>
  <div class="email-sender-container">
    <header class="header">
      <h1>Marketing Email Creator</h1>
      <p class="subtitle">Create and compose your campaigns</p>
    </header>

    <div class="main-layout">
      <!-- Sidebar -->
      <aside class="sidebar">
        <!-- Stats Card -->
        <div class="card stats-card">
          <h3>Campaign Stats</h3>
          <div class="stat-item">
            <span class="stat-label">Subscribers</span>
            <span class="stat-value">{{ stats.totalSubscribers.toLocaleString() }}</span>
          </div>
          <div class="stat-item">
            <span class="stat-label">Avg. Open Rate</span>
            <span class="stat-value">{{ stats.openRate }}%</span>
          </div>
          <div class="stat-item">
            <span class="stat-label">Avg. Click Rate</span>
            <span class="stat-value">{{ stats.clickRate }}%</span>
          </div>
        </div>

        <!-- Segments -->
        <div class="card">
          <h3>Target Audience</h3>
          <div class="segment-list">
            <button
              v-for="segment in segments"
              :key="segment.id"
              @click="selectSegment(segment.id)"
              :class="{ active: selectedSegment === segment.id }"
              class="segment-btn"
            >
              <span class="segment-name">{{ segment.name }}</span>
              <span class="segment-count">{{ segment.count.toLocaleString() }}</span>
            </button>
          </div>
        </div>

        <!-- Automation -->
        <div class="card">
          <h3>Schedule Send</h3>
          <div class="send-options">
            <label class="radio-option">
              <input v-model="sendTime" type="radio" value="now" />
              <span>Send Now</span>
            </label>
            <label class="radio-option">
              <input v-model="sendTime" type="radio" value="schedule" />
              <span>Schedule for Later</span>
            </label>
            <label class="radio-option">
              <input v-model="sendTime" type="radio" value="automation" />
              <span>Set as Automation</span>
            </label>
          </div>
        </div>
      </aside>

      <!-- Main Form -->
      <main class="content">
        <form @submit.prevent class="email-form">
          <div class="form-group">
            <label for="from">From:</label>
            <input
              id="from"
              v-model="email.from"
              type="email"
              placeholder="sender@example.com"
              required
            />
          </div>

          <div class="form-group">
            <label for="to">To:</label>
            <input
              id="to"
              v-model="email.to"
              type="email"
              placeholder="recipient@example.com"
              required
            />
          </div>

          <div class="form-group">
            <label for="subject">Subject:</label>
            <input
              id="subject"
              v-model="email.subject"
              type="text"
              placeholder="Enter email subject"
              required
            />
          </div>

          <div class="form-group full-width">
            <label for="content">Content:</label>
            <textarea
              id="content"
              v-model="email.content"
              placeholder="Enter your email content here..."
              rows="12"
            ></textarea>
          </div>

          <div class="button-group">
            <button type="button" class="btn btn-reset" @click="resetForm">Reset</button>
            <button type="button" class="btn btn-primary">Send Email</button>
          </div>
        </form>
      </main>
    </div>
  </div>
</template>
