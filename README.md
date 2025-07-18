# Dr. Kathryn Loosemore PhD - Academic Website

[![Netlify Status](https://api.netlify.com/api/v1/badges/81c523d9-0698-42e5-8f6e-cb12531c7023/deploy-status)](https://app.netlify.com/projects/kloosemore/deploys)

This is the source code for Dr. Kathryn Loosemore's personal academic website, focusing on her research in International Relations, particularly regarding ETA (Euskadi Ta Askatasuna) terrorism studies.

## Hosting

This site is hosted by [Netlify](https://app.netlify.com/projects/kloosemore) and auto-deploys on push to the `main` branch.

## Tech Stack

- **Hugo**: Static site generator (minimum version 0.112.0)
- **Theme**: Salinger - a clean, minimalistic, mobile-first Hugo theme
- **CSS Framework**: TailwindCSS with DaisyUI components
- **Node.js**: v22.11.0 (for build tooling)

## Development

### Initial Setup
```bash
# Install Hugo module dependencies
hugo mod npm pack

# Install npm dependencies
npm install
```

### Development
```bash
# Start development server
hugo server

# Start development server with drafts
hugo server --buildDrafts
```

### Build
```bash
# Build the static site (outputs to /public)
hugo
```

## Project Structure

- `/content/`: All website content in Markdown format
- `/themes/salinger/`: Theme directory
- `/static/`: Static files served directly
- `/public/`: Build output

## Contact Form

The site includes a contact form integrated with Netlify Forms for secure message handling:

- **Location**: Available at `/contact/` with links in header and footer navigation
- **Features**: Spam protection via honeypot field, form validation, custom success page
- **Privacy**: Email address is completely hidden from source code
- **Submissions**: All form submissions appear in the Netlify dashboard under Forms section
- **Notifications**: Email notifications can be configured in Netlify site settings

### Form Management

- **View submissions**: Netlify Dashboard → Site → Forms
- **Configure notifications**: Site Settings → Forms → Form notifications
- **Spam filtering**: Automatic spam detection with manual review options
- **Export data**: Submissions can be exported from the Netlify dashboard

## Content Focus

The website serves as both a portfolio and research repository, with particular emphasis on ETA terrorism studies and victim databases. All content maintains a formal academic tone appropriate for professional academic presentation.