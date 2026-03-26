# Heart & Stroke Survey Platform

A modern, interactive survey web application built as a POC, powered by Next.js and Contentful CMS. This platform enables dynamic survey creation and management through a headless CMS, providing a seamless user experience with server-side rendering and incremental static regeneration.

## 🚀 Features

- **Dynamic Survey Management**: Survey questions and content managed through Contentful CMS
- **Incremental Static Regeneration (ISR)**: Automatic content updates every 30 seconds
- **Dynamic Routing**: Seamless navigation through survey questions
- **Server-Side Rendering**: Optimized performance with Next.js App Router
- **TypeScript**: Full type safety throughout the application
- **Responsive Design**: Modern UI built with Tailwind CSS and CSS Modules

## 🛠️ Tech Stack

- **Framework**: [Next.js 15](https://nextjs.org/) with App Router
- **Language**: TypeScript
- **UI**: React 19, Tailwind CSS, CSS Modules
- **CMS**: [Contentful](https://www.contentful.com/)
- **Deployment**: Azure Static Web Apps
- **Font**: Geist (optimized with `next/font`)

## 📋 Prerequisites

Before you begin, ensure you have:

- Node.js 20+ installed
- npm, yarn, pnpm, or bun package manager
- Contentful account with:
  - Space ID
  - Content Delivery API access token
- Azure account (for deployment)

## 🔧 Getting Started

### 1. Clone the Repository

```bash
git clone <repository-url>
cd heart-stroke-survey-platform
```

### 2. Install Dependencies

```bash
npm install
# or
yarn install
# or
pnpm install
# or
bun install
```

### 3. Environment Variables

Create a `.env.local` file in the root directory:

```env
CONTENTFUL_SPACE_ID=your_contentful_space_id
CONTENTFUL_ACCESS_TOKEN=your_contentful_access_token
```

### 4. Run Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to see the application.

## 📁 Project Structure

```
├── app/                      # Next.js App Router pages
│   ├── page.tsx             # Home page (SSR)
│   ├── static/              # Static ISR page
│   └── survey/
│       └── question/
│           └── [slug]/      # Dynamic question pages
├── components/               # React components
│   ├── Header/              # Survey header component
│   ├── RoutingButton/       # Navigation button component
│   └── SurveyQuestion/      # Question display component
├── contentful/               # Contentful client configuration
│   └── client.ts            # Contentful API client
├── public/                  # Static assets
└── .github/
    └── workflows/           # CI/CD workflows
```

## 🏗️ Architecture

### Content Model

The application expects the following Contentful content types:

- **Survey**: Contains survey metadata (title, description, firstQuestion)
- **Question**: Individual survey questions with:
  - `title`: Question text
  - `slug`: Unique identifier for routing
  - `nextQuestion`: Reference to the next question

### Rendering Strategy

- **Home Page (`/`)**: Server-Side Rendered (SSR)
- **Static Page (`/static`)**: Incremental Static Regeneration (ISR) with 30s revalidation
- **Question Pages (`/survey/question/[slug]`)**: ISR with 30s revalidation

### Data Fetching

All survey data is fetched from Contentful at build time and runtime, with automatic revalidation every 30 seconds to ensure fresh content.

## 🚢 Deployment

### Azure Static Web Apps

The application is configured for deployment on Azure Static Web Apps via GitHub Actions.

#### Deployment Workflow

1. Push to `main` branch triggers automatic deployment
2. Pull requests create preview deployments
3. Environment variables are configured in GitHub Secrets:
   - `CONTENTFUL_SPACE_ID`
   - `CONTENTFUL_ACCESS_TOKEN`
   - `AZURE_STATIC_WEB_APPS_API_TOKEN_BRAVE_SKY_0ACBF4F10`

#### Manual Deployment

```bash
# Build the application
npm run build

# Start production server
npm start
```

## 📝 Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm start` - Start production server
- `npm run lint` - Run ESLint

## 🔐 Environment Variables

| Variable                  | Description                           | Required |
| ------------------------- | ------------------------------------- | -------- |
| `CONTENTFUL_SPACE_ID`     | Your Contentful space ID              | Yes      |
| `CONTENTFUL_ACCESS_TOKEN` | Contentful Content Delivery API token | Yes      |

## 🧪 Development

### Adding New Questions

1. Create a new Question entry in Contentful
2. Set the `slug` field (used for routing)
3. Link questions using the `nextQuestion` reference field
4. The application will automatically pick up new questions on the next revalidation cycle

### Customizing Styles

- Global styles: `app/globals.css`
- Component styles: Individual `.module.css` files in component directories
- Tailwind configuration: `tailwind.config.ts`

## 🤝 Contributing

1. Create a feature branch from `main`
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## 📄 License

This project is private and proprietary.
