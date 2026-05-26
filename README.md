# Vue 3 + Vite Email Creator Demo: Campaign Builder with Email Marketing Features

This is a [Vue 3](https://vuejs.org/) project bootstrapped with [create-vue](https://github.com/vuejs/create-vue) and [Vite](https://vitejs.dev/). It provides a clean, no-frills email campaign creator interface with integrated marketing features in a sidebar.

## Features

- **Email Campaign Creator**: Simple form for composing emails with From, To, Subject, and Content fields
- **Campaign Stats**: Display subscriber counts and average engagement metrics
- **Email Templates**: Pre-built template options (Welcome Series, Promotional, Newsletter, Abandoned Cart)
- **Audience Segmentation**: Target different subscriber segments (All, Active, Inactive, Premium)
- **Send Scheduling**: Options to send immediately, schedule for later, or set up automation
- **Responsive Design**: Works seamlessly on desktop and mobile devices
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

## Recommended IDE Setup

[VS Code](https://code.visualstudio.com/) + [Vue (Official)](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customization

### Replacing the Textarea

The email content field uses a plain `<textarea>` element. You can easily replace it with a rich text editor like [TinyMCE](https://www.tiny.cloud/), [Quill](https://quilljs.com/), or [Monaco Editor](https://microsoft.github.io/monaco-editor/).

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
