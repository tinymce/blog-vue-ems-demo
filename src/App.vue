<script setup lang="ts">
import { ref } from 'vue'
import Editor from '@tinymce/tinymce-vue'

const email = ref({
  from: '',
  to: '',
  subject: '',
  content: ''
})

const selectedTemplate = ref<string | null>(null)
const selectedSegment = ref<string | null>(null)
const sendTime = ref('now')

const templates = [
  { id: 'welcome', name: 'Welcome Series', emails: 3 },
  { id: 'promo', name: 'Promotional', emails: 1 },
  { id: 'newsletter', name: 'Newsletter', emails: 12 },
  { id: 'abandoned', name: 'Abandoned Cart', emails: 2 }
]

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

const advtemplate_templates = [
  {
    title: 'Customer onboarding',
    items: [
      {
        title: 'Welcome new subscriber',
        content:
          '<p><strong>Welcome to the Brightside community!</strong></p><p>Thanks for joining our list. You\'ll be the first to hear about fresh launches, limited offers, and behind-the-scenes updates.</p><p>Talk soon,<br />The Brightside Team 🌞</p>'
      },
      {
        title: 'First purchase thank-you',
        content:
          '<p><strong>You did it, your order is on the way!</strong></p><p>Hi {{First Name}}, thank you for trusting Brightside with your first purchase. As a welcome gift, enjoy <strong>15% off</strong> your next order with code <span style="background-color:#fef3c7;padding:2px 6px;border-radius:4px;">HELLOAGAIN</span>.</p>'
      }
    ]
  },
  {
    title: 'Promotions & launches',
    items: [
      {
        title: 'Product launch spotlight',
        content:
          '<p><strong>Introducing the Glow Serum</strong></p><p>Meet the newest member of our skincare lineup: a vitamin C powerhouse that brightens, hydrates, and defends your skin in just one pump.</p>'
      },
      {
        title: '72-hour flash sale',
        content:
          '<p><strong>72-Hour Flash Sale Starts Now!</strong></p><p>Gear up for the season with sitewide savings, <strong>up to 35% off</strong>.</p>'
      }
    ]
  }
]

const mergetags_list = [
  {
    title: 'Customer',
    menu: [
      { value: 'First Name', title: 'First Name' },
      { value: 'Company Name', title: 'Company Name' },
      { value: 'Email Address', title: 'Email Address' }
    ]
  },
  {
    title: 'Compliance & Footer',
    menu: [
      { value: 'Unsubscribe Link', title: 'Unsubscribe' },
      { value: 'Update Preferences', title: 'Update Preferences' },
      { value: 'Company Address', title: 'Company Address' }
    ]
  }
]

const resetForm = () => {
  email.value = {
    from: '',
    to: '',
    subject: '',
    content: ''
  }
}

const applyTemplate = (templateId: string) => {
  selectedTemplate.value = templateId
  const template = templates.find(t => t.id === templateId)
  if (template) {
    email.value.subject = `${template.name} - Draft`
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

        <!-- Templates -->
        <div class="card">
          <h3>Templates</h3>
          <div class="template-list">
            <button
              v-for="template in templates"
              :key="template.id"
              @click="applyTemplate(template.id)"
              :class="{ active: selectedTemplate === template.id }"
              class="template-btn"
            >
              <span class="template-name">{{ template.name }}</span>
              <span class="template-count">{{ template.emails }}</span>
            </button>
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
            <editor
              api-key="pv55e7h13r9k5kdv7tehf4c1zwmzep2kt59byp0r6qsjadjm"
              v-model="email.content"
              :init="{
                height: 500,
                menubar: false,
                plugins:
                  'mergetags advtemplate inlinecss fullpagehtml advlist autolink link image lists charmap preview anchor searchreplace visualblocks code fullscreen insertdatetime media table help wordcount',
                toolbar:
                  'mergetags inserttemplate | fullpagehtml undo redo | styles | bold italic underline | alignleft aligncenter alignright | bullist numlist outdent indent | link image | code preview',
                advtemplate_templates,
                mergetags_list
              }"
            />
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
