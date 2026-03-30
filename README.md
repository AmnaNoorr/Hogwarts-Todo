# The Enchanted Task Hall 🧙‍♂️

A magical todo application themed around the Harry Potter universe, hosted on Firebase Hosting.

## Project Overview

**The Enchanted Task Hall** is a beautifully styled, interactive todo application with a Harry Potter theme. Users can create, manage, and complete tasks organized by magical categories (houses). The application features enchanting visual effects including aurora effects, twinkling stars, shooting stars, and ember particles to create an immersive wizarding experience.

### Key Features

- 📝 **Create and Manage Tasks**: Add tasks with titles, priorities, and due dates
- 🏰 **House Categories**: Organize tasks by Hogwarts houses (Gryffindor, Hufflepuff, Ravenclaw, Slytherin)
- ✨ **Magical Visual Effects**: Aurora, stars, shooting stars, and ember animations
- 🌙 **Enchanted UI**: Beautiful parchment-style cards with gold accents and Harry Potter fonts
- ✅ **Task Progress Tracking**: Progress orb showing completion status
- 💾 **Local Storage**: Persists tasks in browser local storage

## Architecture

### Technology Stack

- **Frontend**: Vanilla HTML, CSS, and JavaScript (ES6+)
- **Hosting**: Firebase Hosting
- **Version Control**: Git/GitHub
- **CI/CD**: GitHub Actions

### Project Structure

```
Hogwarts-Todo/
├── public/                          # Firebase hosting root directory
│   └── index.html                  # Single-page application with all HTML, CSS, and JS
├── .github/
│   └── workflows/                  # GitHub Actions workflows
│       ├── firebase-hosting-merge.yml      # Production deployment on main branch
│       └── firebase-hosting-pull-request.yml  # Preview deployment on pull requests
├── firebase.json                   # Firebase configuration
├── .firebaserc                     # Firebase project settings
├── .gitignore                      # Git ignore rules
└── README.md                       # This file
```

### Frontend Architecture

The application is built as a **Single-Page Application (SPA)** with the following structure:

#### HTML Structure
- **Animated Background**: Sky, aurora, stars, shooting stars, and embers
- **Moon**: Fixed moon element for ambiance
- **Stage**: Container for dynamic card elements
- **Progress Orb**: Visual indicator of task completion progress
- **Control Panel**: Task input interface with category and priority selection

#### CSS Architecture
- **CSS Variables (Custom Properties)**: Define magical color scheme
  - Navy background (`--navy`)
  - Gold accents (`--gold`, `--goldglow`)
  - Parchment color (`--parch`)
  - Category-specific colors for Hogwarts houses

- **Animations & Effects**:
  - Aurora drift animation
  - Star twinkling effect
  - Shooting star trajectory
  - Ember rising animation
  - Card pulse effect on completion
  - Candle flame flicker animation

#### JavaScript Functionality
- **Task Management**: CRUD operations (Create, Read, Update, Delete)
- **Local Storage**: Persists tasks between sessions
- **Card Rendering**: Dynamically creates task cards with animations
- **Event Handling**: Click handlers for checkboxes, task completion, and deletion
- **Visual Effects**: Generates and animates particles (embers, sparks, shooting stars)
- **Progress Calculation**: Tracks and displays task completion percentage

### Data Model

Tasks are stored with the following structure:
```javascript
{
  id: unique_identifier,
  text: "task description",
  category: "house_name",     // Gryffindor, Hufflepuff, Ravenclaw, Slytherin
  priority: emoji,            // 🔥, 💛, 💙, 💚
  done: boolean,              // completion status
  due: "date_string"          // optional due date
}
```

## CI/CD Pipelines

The project uses **GitHub Actions** for automated deployment with two workflows:

### 1. Production Deployment: `firebase-hosting-merge.yml`

**Trigger**: Push to `main` branch

**Steps**:
- Checkout repository code
- Deploy to Firebase Hosting using `FirebaseExtended/action-hosting-deploy@v0`
- Uses `FIREBASE_SERVICE_ACCOUNT_HOGWARTS_TODO` secret for authentication
- Deploys to production channel (live)

**Environment**:
- Runs on: `ubuntu-latest`
- Project ID: `hogwarts-todo`

### 2. Preview Deployment: `firebase-hosting-pull-request.yml`

**Trigger**: Pull requests targeting the repository

**Steps**:
- Checkout pull request code
- Install dependencies: `npm ci`
- Build project: `npm run build`
- Deploy preview to Firebase Hosting
- Creates preview URL for testing
- Posts preview link to PR for review

**Environment**:
- Runs on: `ubuntu-latest`
- Project ID: `hogwarts-todo`
- Permissions: write checks, read contents, write pull-requests

**Security Notes**:
- Only runs if PR is from the same repository
- Uses `GITHUB_TOKEN` and Firebase service account secrets
- Preview deployments are temporary and auto-cleaned

## Installation & Setup

### Prerequisites

- Git
- Firebase CLI (for local testing)
- Modern web browser

### Local Development

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/Hogwarts-Todo.git
   cd Hogwarts-Todo
   ```

2. **Open locally** (no build step required):
   ```bash
   # Option 1: Open public/index.html directly in your browser
   open public/index.html

   # Option 2: Use Firebase emulator for testing
   firebase use hogwarts-todo
   firebase serve
   ```

3. **The application will be available at**:
   - Direct: `file:///path/to/Hogwarts-Todo/public/index.html`
   - Firebase serve: `http://localhost:5000`

### Firebase Configuration

- **Project ID**: `hogwarts-todo`
- **Hosting Region**: Firebase default
- **Rewrites**: All requests route to `/index.html` (SPA configuration)
- **Public Directory**: `public/`

## Deployment

### Automatic Deployment

The application automatically deploys when:

1. **Production** 🚀:
   - Code is merged to `main` branch
   - GitHub Actions runs the merge workflow
   - Updates live Firebase Hosting channel

2. **Preview** 👀:
   - Pull request is created
   - Automatic preview deployment created
   - Preview URL posted to PR
   - Expires after PR is closed

### Manual Deployment

To deploy manually:

```bash
# Install Firebase CLI if not already installed
npm install -g firebase-tools

# Login to Firebase
firebase login

# Deploy to Firebase Hosting
firebase deploy --project hogwarts-todo
```

## Environment Variables & Secrets

### GitHub Secrets Required

For CI/CD pipelines to work, the following secrets must be configured in GitHub:

1. **`FIREBASE_SERVICE_ACCOUNT_HOGWARTS_TODO`**: Firebase service account JSON key for authentication
   - Generated from Firebase Console → Project Settings → Service Accounts

2. **`GITHUB_TOKEN`**: Automatically provided by GitHub Actions (no setup needed)

### Setting up Secrets

1. Go to GitHub repository → Settings → Secrets and variables → Actions
2. Add new secret: `FIREBASE_SERVICE_ACCOUNT_HOGWARTS_TODO`
3. Paste Firebase service account JSON key
4. Save

## Browser Support

- Modern browsers with ES6 support
- CSS Grid and Flexbox support
- CSS custom properties (variables) support
- Local Storage support

Tested on:
- Chrome/Chromium 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## File Configurations

### `firebase.json`

Configures Firebase Hosting behavior:
- **Public directory**: `public`
- **SPA rewrites**: Routes all requests to `index.html`
- **Ignore files**: Excludes config files and node_modules from deployment

### `.firebaserc`

Specifies active Firebase project:
- **Default project**: `hogwarts-todo`

## Contributing

1. Create a feature branch from `main`
2. Make your changes
3. Push to your branch
4. Create a Pull Request
5. Preview deployment will be automatically created
6. Merge to `main` after review for production deployment

## Performance Notes

- **Static Site**: No server-side rendering, fast load times
- **Local Storage**: Tasks persist without backend calls
- **Bundling**: Single HTML file with embedded CSS and JavaScript
- **Animations**: GPU-accelerated CSS animations for smooth performance
- **No Build Step Required**: Ready to deploy as-is

## Future Enhancements

Potential features for improvement:
- Backend integration (Firebase Realtime Database or Firestore)
- User authentication (Firebase Auth)
- Multi-device synchronization
- Task sharing and collaboration
- Recurring tasks and reminders
- Dark/Light mode toggle
- Task tags and filtering



**Deploy Status**: [![Firebase Hosting](https://github.com/yourusername/Hogwarts-Todo/workflows/Deploy%20to%20Firebase%20Hosting/badge.svg)](https://github.com/yourusername/Hogwarts-Todo/actions)

**Live Application**: [The Enchanted Task Hall](https://hogwarts-todo.web.app)
