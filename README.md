# Vue 3 + Vite Email Creator Demo: Campaign Builder with Email Marketing Features

This is a [Vue 3](https://vuejs.org/) project bootstrapped with [create-vue](https://github.com/vuejs/create-vue) and [Vite](https://vitejs.dev/). It provides a clean, no-frills email campaign creator interface with integrated marketing features in a sidebar.

## Features

**Functional:**

- **Email Creator Form**: Simple form for composing emails with From, To, Subject, and Content fields

**UI Mockups** (Demo sidebar interface - ready for your implementation):

- **Campaign Stats**: Displays sample subscriber counts and engagement metrics
- **Email Templates**: Visual selector for template options (Welcome Series, Promotional, Newsletter, Abandoned Cart)
- **Audience Segmentation**: UI for targeting different subscriber segments (All, Active, Inactive, Premium)
- **Send Scheduling**: Options to choose send timing (Now, Schedule, Automation)

**Design:**

- **Responsive Layout**: Works seamlessly on desktop and mobile devices
- **Lavender & Red Theme**: Modern color scheme with gradients and smooth interactions

## Getting Started

1. Install dependencies:

```bash
npm install
```

2. Run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:5174](http://localhost:5174) with your browser to see the result.

3. Build for production:

```bash
npm run build
```

## Project Structure

```
src/
├── App.vue           # Main email creator component
├── main.ts           # Application entry point
└── styles.css        # Centralized styling
```

## About the UI Mockups

The sidebar contains demo UI elements with sample data to showcase what a full email marketing system could look like. These are **visual mockups only**—they don't connect to any backend. You can:

- Click templates and segments to see the UI respond
- Use these as a blueprint for building out real functionality
- Wire them up to your own backend API or email service

This is intentionally a **no-frills starting point** for you to build upon.

## Recommended IDE Setup

[VS Code](https://code.visualstudio.com/) + [Vue (Official)](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customization

### Replacing the Textarea

The email content field uses a plain `<textarea>` element. Follow the tutorial on [TinyMCE's blog](https://www.tiny.cloud/blog/) to add a rich text editor to your email marketing app.

### Integrating Email Service

The `Send Email` button is ready for integration with any email service. The email data is stored in the reactive `email` object:

```typescript
email.value = {
  from: "string",
  to: "string",
  subject: "string",
  content: "string",
};
```

You can connect it to services like:

- [Resend](https://resend.com/)
- [SendGrid](https://sendgrid.com/)
- [Mailgun](https://www.mailgun.com/)
- Your own backend API

## Learn More

To learn more about the technologies used:

- [Vue 3 Documentation](https://vuejs.org/) - Learn about Vue 3 features and API
- [Vite Documentation](https://vitejs.dev/) - Understand Vite's features and configuration
- [TypeScript Handbook](https://www.typescriptlang.org/docs/) - Learn TypeScript basics
- [Email Marketing Best Practices](https://mailchimp.com/resources/) - Explore email campaign strategies

## Deployment

The app can be deployed to any static hosting service:

- [Vercel](https://vercel.com/)
- [Netlify](https://www.netlify.com/)
- [GitHub Pages](https://pages.github.com/)
- [AWS S3](https://aws.amazon.com/s3/)

Build the project and deploy the `dist` folder to your hosting provider.

## License

MIT
