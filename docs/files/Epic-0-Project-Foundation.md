# Epic 0: Project Foundation

## Epic Metadata

| Field                  | Value                        |
| ---------------------- | ---------------------------- |
| **Epic ID**            | Epic 0                       |
| **Epic Name**          | Project Foundation           |
| **Priority**           | P0 (Critical)                |
| **Status**             | Ready for Development        |
| **Estimated Duration** | 1-2 weeks                    |
| **Dependencies**       | None (first epic)            |
| **Owner**              | Tech Lead + Development Team |

---

## Epic Overview

### Purpose

Establish the foundational project structure, tooling, and development environment for GameDuel. This epic ensures all developers have a consistent, properly configured codebase before implementing features.

### Business Value

- **Risk Mitigation**: Prevents inconsistent setups that cause integration issues
- **Development Velocity**: Clear structure accelerates feature development
- **Code Quality**: Linting, formatting, and testing infrastructure from day one
- **Team Alignment**: All developers work from identical configuration

### Success Criteria

- ✅ Project builds successfully on all developer machines
- ✅ Linting and formatting work automatically
- ✅ Test infrastructure runs successfully
- ✅ Directory structure matches architecture document
- ✅ All core dependencies installed and working
- ✅ CI/CD pipeline successfully builds the app

### Epic Acceptance Criteria

- [ ] `npm start` launches Expo development server successfully
- [ ] `npm run lint` executes without errors
- [ ] `npm test` runs Jest tests successfully
- [ ] Project structure matches Architecture Section 5.2
- [ ] GitHub Actions workflow builds project successfully
- [ ] README contains setup instructions for new developers

---

## Stories in This Epic

1. **Story 0.1**: Initialize Expo Project
2. **Story 0.2**: Configure Code Quality Tools
3. **Story 0.3**: Set Up Project Directory Structure
4. **Story 0.4**: Install Core Dependencies
5. **Story 0.5**: Configure Testing Infrastructure
6. **Story 0.6**: Set Up CI/CD Pipeline
7. **Story 0.7**: Create Project Documentation

---

## Story 0.1: Initialize Expo Project

### Story Metadata

```yaml
id: story-0.1
title: Initialize Expo Project with TypeScript
epic: Epic 0 - Project Foundation
priority: P0
estimated_effort: 2-4 hours
dependencies: []
assignee: Tech Lead
status: Ready
```

### User Story

**As a** developer  
**I want** a properly initialized Expo project with TypeScript  
**So that** I can start building features with type safety and modern tooling

### Context

This is the first story in the entire project. We need to create the base React Native project using Expo's managed workflow with TypeScript support.

### Acceptance Criteria

- [ ] Expo project initialized using `npx create-expo-app gameduel --template expo-template-blank-typescript`
- [ ] Project runs successfully with `npm start`
- [ ] TypeScript compilation works without errors
- [ ] Expo SDK version is 54 (as specified in Architecture Section 4.1)
- [ ] Initial `App.tsx` displays "Welcome to GameDuel" on screen
- [ ] Project can be previewed on both iOS Simulator and Android Emulator
- [ ] Git repository initialized with initial commit

### Technical Implementation Notes

**Commands to Execute:**

```bash
# Initialize project
npx create-expo-app gameduel --template expo-template-blank-typescript

cd gameduel

# Verify Expo SDK version
npx expo --version  # Should be SDK 54

# Test the app
npm start

# Initialize git
git init
git add .
git commit -m "Initial project setup with Expo + TypeScript"
```

**Expected Project Structure After Initialization:**

```
gameduel/
├── App.tsx                 # Main entry point
├── app.json                # Expo configuration
├── package.json            # Dependencies
├── tsconfig.json           # TypeScript config
├── babel.config.js         # Babel config
├── node_modules/
├── assets/
│   ├── icon.png
│   ├── splash.png
│   └── adaptive-icon.png
└── .gitignore
```

**Verification Steps:**

1. Run `npm start` - Expo DevTools should open
2. Press `i` for iOS simulator - App should load
3. Press `a` for Android emulator - App should load
4. Verify TypeScript is working: Add type error in App.tsx, should show red squiggly

### Definition of Done

- [ ] Project initializes without errors
- [ ] App runs on iOS Simulator
- [ ] App runs on Android Emulator
- [ ] TypeScript compilation successful
- [ ] Git repository created with initial commit
- [ ] README.md contains basic project information
- [ ] Code reviewed by Tech Lead
- [ ] Changes committed to `main` branch

### Blockers / Dependencies

- **None** - This is the first story

### Notes

- Use the TypeScript template (not JavaScript)
- Ensure Node version is 18+ (as per Architecture requirements)
- If Expo CLI not installed globally: `npm install -g expo-cli`

---

## Story 0.2: Configure Code Quality Tools

### Story Metadata

```yaml
id: story-0.2
title: Configure ESLint, Prettier, and Git Hooks
epic: Epic 0 - Project Foundation
priority: P0
estimated_effort: 3-4 hours
dependencies: [story-0.1]
assignee: Tech Lead
status: Ready
```

### User Story

**As a** developer  
**I want** automated code quality tools configured  
**So that** the codebase maintains consistent style and catches errors early

### Context

Per Architecture Section 11.1-11.3, we need ESLint for code quality, Prettier for formatting, and git hooks to enforce standards before commits.

### Acceptance Criteria

- [ ] ESLint installed and configured with React Native + TypeScript rules
- [ ] Prettier installed and configured with project style guide
- [ ] Husky installed for git hooks
- [ ] Pre-commit hook runs lint and format checks
- [ ] `npm run lint` command executes ESLint successfully
- [ ] `npm run format` command formats code with Prettier
- [ ] `npm run lint:fix` auto-fixes linting errors
- [ ] VS Code settings configured for auto-format on save
- [ ] Configuration files match Architecture Section 11.1

### Technical Implementation Notes

**Dependencies to Install:**

```bash
npm install --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser
npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
npm install --save-dev eslint-plugin-react eslint-plugin-react-hooks
npm install --save-dev husky lint-staged
```

**ESLint Configuration** (.eslintrc.json):

```json
{
  "extends": ["expo", "prettier"],
  "plugins": ["prettier", "react-hooks"],
  "rules": {
    "prettier/prettier": "error",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "no-console": ["warn", { "allow": ["warn", "error"] }],
    "@typescript-eslint/no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
    "import/order": [
      "error",
      {
        "groups": ["builtin", "external", "internal", "parent", "sibling", "index"],
        "newlines-between": "always",
        "alphabetize": { "order": "asc" }
      }
    ]
  }
}
```

**Prettier Configuration** (.prettierrc):

```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "arrowParens": "always"
}
```

**Package.json Scripts:**

```json
{
  "scripts": {
    "lint": "eslint . --ext .ts,.tsx",
    "lint:fix": "eslint . --ext .ts,.tsx --fix",
    "format": "prettier --write \"**/*.{ts,tsx,json,md}\"",
    "format:check": "prettier --check \"**/*.{ts,tsx,json,md}\"",
    "prepare": "husky install"
  }
}
```

**Husky Pre-commit Hook:**

```bash
# Initialize husky
npx husky install

# Create pre-commit hook
npx husky add .husky/pre-commit "npx lint-staged"
```

**lint-staged Configuration** (package.json):

```json
{
  "lint-staged": {
    "*.{ts,tsx}": ["eslint --fix", "prettier --write"],
    "*.{json,md}": ["prettier --write"]
  }
}
```

**VS Code Settings** (.vscode/settings.json):

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

### Verification Steps

1. Create a file with intentional style violations
2. Run `npm run lint` - should show errors
3. Run `npm run lint:fix` - should auto-fix
4. Attempt commit with errors - pre-commit hook should block
5. Fix errors and commit - should succeed

### Definition of Done

- [ ] ESLint configuration file created
- [ ] Prettier configuration file created
- [ ] Husky git hooks installed
- [ ] Pre-commit hook prevents bad commits
- [ ] Package.json scripts added
- [ ] VS Code settings configured
- [ ] Documentation added to README
- [ ] All existing code passes linting
- [ ] Code reviewed and merged

### Blockers / Dependencies

- **Requires**: Story 0.1 (project must exist)

### Notes

- Follow exact configuration from Architecture Section 11.1
- Test pre-commit hook by intentionally breaking style
- Ensure all team members install VS Code Prettier extension

---

## Story 0.3: Set Up Project Directory Structure

### Story Metadata

```yaml
id: story-0.3
title: Create Project Directory Structure
epic: Epic 0 - Project Foundation
priority: P0
estimated_effort: 2-3 hours
dependencies: [story-0.1]
assignee: Tech Lead
status: Ready
```

### User Story

**As a** developer  
**I want** the project directory structure to match the architecture  
**So that** I know exactly where to place new files and code

### Context

Architecture Section 5.2 defines a comprehensive directory structure. We need to create all folders and placeholder files with README.md in each directory explaining its purpose.

### Acceptance Criteria

- [ ] All directories from Architecture Section 5.2 created
- [ ] Each major directory contains README.md explaining its purpose
- [ ] Placeholder index.ts files in appropriate directories
- [ ] `.gitkeep` files in empty directories to preserve in git
- [ ] Directory structure exactly matches architecture diagram
- [ ] Path aliases configured in tsconfig.json
- [ ] Import examples work (e.g., `import { Button } from '@/components/common/Button'`)

### Technical Implementation Notes

**Directory Structure to Create:**

```
src/
├── screens/                    # Screen components
│   ├── home/
│   ├── record/
│   ├── gallery/
│   ├── profile/
│   └── auth/
├── components/                 # Reusable components
│   ├── common/
│   │   ├── Button/
│   │   ├── Card/
│   │   ├── Input/
│   │   └── LoadingIndicator/
│   ├── video/
│   │   ├── VideoCard/
│   │   ├── VideoPlayer/
│   │   └── RecordingTimer/
│   └── gaming/
│       ├── GamingAccountCard/
│       ├── AchievementBadge/
│       └── StatDisplay/
├── navigation/                 # Navigation setup
├── contexts/                   # React Context providers
├── hooks/                      # Custom React hooks
├── services/                   # Business logic services
│   ├── auth/
│   ├── video/
│   └── gaming/
├── repositories/               # Data access layer
├── api/                        # External API clients
│   ├── steam/
│   ├── xbox/
│   └── psn/
├── storage/                    # Storage abstraction
├── models/                     # TypeScript types/interfaces
├── utils/                      # Utility functions
├── theme/                      # App theming
├── config/                     # App configuration
└── __tests__/                  # Test utilities
    ├── mocks/
    └── helpers/

assets/                         # Static assets
├── images/
├── icons/
└── fonts/

docs/                           # Documentation
```

**Create Script** (create-structure.sh):

```bash
#!/bin/bash

# Create all directories
mkdir -p src/{screens/{home,record,gallery,profile,auth},components/{common/{Button,Card,Input,LoadingIndicator},video/{VideoCard,VideoPlayer,RecordingTimer},gaming/{GamingAccountCard,AchievementBadge,StatDisplay}},navigation,contexts,hooks,services/{auth,video,gaming},repositories,api/{steam,xbox,psn},storage,models,utils,theme,config,__tests__/{mocks,helpers}}

mkdir -p assets/{images,icons,fonts}
mkdir -p docs

# Create .gitkeep files in empty directories
find src -type d -empty -exec touch {}/.gitkeep \;
find assets -type d -empty -exec touch {}/.gitkeep \;

echo "Directory structure created successfully!"
```

**README Template for Each Directory:**

```markdown
# [Directory Name]

## Purpose

[Brief description of what files belong here]

## Examples

[Examples of files that should be in this directory]

## Related Documentation

- [Link to relevant architecture section]
```

**tsconfig.json Path Aliases:**

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
      "@components/*": ["./src/components/*"],
      "@screens/*": ["./src/screens/*"],
      "@services/*": ["./src/services/*"],
      "@hooks/*": ["./src/hooks/*"],
      "@models/*": ["./src/models/*"],
      "@utils/*": ["./src/utils/*"],
      "@theme/*": ["./src/theme/*"],
      "@config/*": ["./src/config/*"],
      "@navigation/*": ["./src/navigation/*"],
      "@contexts/*": ["./src/contexts/*"],
      "@api/*": ["./src/api/*"],
      "@storage/*": ["./src/storage/*"],
      "@repositories/*": ["./src/repositories/*"]
    }
  }
}
```

**Example README Files to Create:**

**/src/screens/README.md:**

```markdown
# Screens

## Purpose

Screen components represent full-page views in the application. Each screen typically corresponds to a route in the navigation.

## Structure

Each screen should have its own folder containing:

- `[ScreenName].tsx` - Main screen component
- `[ScreenName].styles.ts` - Screen-specific styles
- `[ScreenName].test.tsx` - Screen tests (optional for MVP)

## Examples

- `home/HomeScreen.tsx`
- `record/RecordScreen.tsx`
- `gallery/GalleryScreen.tsx`

## Guidelines

- Screens orchestrate multiple components
- Screens connect to contexts and hooks
- Screens should NOT contain business logic (use services/hooks)
- Keep screens focused on composition and layout

## Related Documentation

- Architecture Section 6.1.1 (Screen Components)
```

**/src/components/README.md:**

```markdown
# Components

## Purpose

Reusable UI components used across multiple screens.

## Structure

- `common/` - Generic components (Button, Card, Input, etc.)
- `video/` - Video-specific components
- `gaming/` - Gaming-related components

Each component should have its own folder:

- `[Component].tsx` - Component implementation
- `[Component].styles.ts` - Component styles
- `[Component].test.tsx` - Component tests

## Guidelines

- Components should be reusable and composable
- Use TypeScript interfaces for props
- Document props with JSDoc comments
- Follow React best practices (memo, useCallback, etc.)

## Related Documentation

- Architecture Section 6.1.2 (Component Hierarchy)
```

### Verification Steps

1. Run `tree src` or `ls -R src` to verify structure
2. Test path alias: Create file `src/utils/test.ts` and import using `@/utils/test`
3. Verify TypeScript recognizes imports
4. Check all directories have README.md

### Definition of Done

- [ ] All directories created
- [ ] README.md in each major directory
- [ ] Path aliases configured
- [ ] Test imports work
- [ ] Documentation updated
- [ ] Code reviewed and merged

### Blockers / Dependencies

- **Requires**: Story 0.1 (project must exist)

### Notes

- Refer to Architecture Section 5.2 for exact structure
- Empty directories need .gitkeep to be tracked by git
- Path aliases improve import readability

---

## Story 0.4: Install Core Dependencies

### Story Metadata

```yaml
id: story-0.4
title: Install Core Dependencies and Libraries
epic: Epic 0 - Project Foundation
priority: P0
estimated_effort: 2-3 hours
dependencies: [story-0.1]
assignee: Developer
status: Ready
```

### User Story

**As a** developer  
**I want** all core dependencies installed and configured  
**So that** I can use them when implementing features

### Context

Architecture Section 4.1 defines the complete technology matrix. We need to install all P0 (critical) dependencies that will be used throughout the project.

### Acceptance Criteria

- [ ] All dependencies from Architecture Section 4.1 installed
- [ ] Package versions match architecture specifications
- [ ] React Navigation configured with basic stack navigator
- [ ] Expo modules installed (camera, av, secure-store, etc.)
- [ ] Type definitions installed for all libraries
- [ ] No dependency version conflicts
- [ ] `npm install` completes without warnings
- [ ] Basic test import works for each library

### Technical Implementation Notes

**Core Dependencies to Install:**

```bash
# Navigation
npm install @react-navigation/native @react-navigation/stack
npm install react-native-screens react-native-safe-area-context

# State Management (built-in React Context - no install needed)

# Storage
npm install @react-native-async-storage/async-storage
npm install expo-secure-store

# Camera & Media
npm install expo-camera
npm install expo-av
npm install expo-media-library
npm install expo-file-system

# OAuth & Browser
npm install expo-web-browser

# HTTP Client
npm install axios

# UI Components
npm install expo-linear-gradient

# Forms & Validation
npm install react-hook-form
npm install zod

# Utilities
npm install uuid
npm install date-fns
```

**Dev Dependencies:**

```bash
# Type Definitions
npm install --save-dev @types/react @types/react-native
npm install --save-dev @types/uuid

# Testing (will configure fully in Story 0.5)
npm install --save-dev jest @testing-library/react-native @testing-library/jest-native

# Already installed in Story 0.2:
# - ESLint, Prettier, Husky, lint-staged
```

**Verify Installation:**

```typescript
// Create src/config/dependencies.test.ts
import AsyncStorage from '@react-native-async-storage/async-storage';
import * as SecureStore from 'expo-secure-store';
import { Camera } from 'expo-camera';
import { Audio, Video } from 'expo-av';
import * as MediaLibrary from 'expo-media-library';
import * as FileSystem from 'expo-file-system';
import * as WebBrowser from 'expo-web-browser';
import axios from 'axios';
import { LinearGradient } from 'expo-linear-gradient';
import { useForm } from 'react-hook-form';
import { z } from 'zod';
import { v4 as uuidv4 } from 'uuid';
import { format } from 'date-fns';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

console.log('All dependencies imported successfully! ✅');
```

**Basic Navigation Setup** (src/navigation/AppNavigator.tsx):

```typescript
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import { Text, View } from 'react-native';

const Stack = createStackNavigator();

// Placeholder screen
const PlaceholderScreen = () => (
  <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
    <Text>Navigation Setup Complete ✅</Text>
  </View>
);

export const AppNavigator = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={PlaceholderScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};
```

**Update App.tsx:**

```typescript
import React from 'react';
import { AppNavigator } from './src/navigation/AppNavigator';

export default function App() {
  return <AppNavigator />;
}
```

**Package.json Verification Script:**

```json
{
  "scripts": {
    "verify-deps": "node -e \"console.log('Verifying dependencies...'); require('./src/config/dependencies.test.ts')\""
  }
}
```

### Verification Steps

1. Run `npm install` - should complete without errors
2. Run `npm start` - app should load
3. Check for dependency warnings in console
4. Verify navigation works (should see "Navigation Setup Complete")
5. Check package-lock.json for version conflicts

### Definition of Done

- [ ] All dependencies installed
- [ ] No version conflicts
- [ ] Basic navigation renders
- [ ] Test imports successful
- [ ] Documentation updated
- [ ] Code reviewed and merged

### Blockers / Dependencies

- **Requires**: Story 0.1 (project must exist)

### Notes

- Exact versions specified in Architecture Section 4.1
- Some dependencies (expo-camera, etc.) require additional native configuration - this happens automatically with Expo
- Navigation setup is minimal for now; will be expanded in Epic 1

---

## Story 0.5: Configure Testing Infrastructure

### Story Metadata

```yaml
id: story-0.5
title: Set Up Jest and Testing Infrastructure
epic: Epic 0 - Project Foundation
priority: P0
estimated_effort: 3-4 hours
dependencies: [story-0.1, story-0.4]
assignee: Developer
status: Ready
```

### User Story

**As a** developer  
**I want** testing infrastructure configured from the start  
**So that** I can write tests alongside features

### Context

Per Architecture Section 11.5, we need Jest for unit/integration tests. This story sets up the testing framework so all future stories can include tests.

### Acceptance Criteria

- [ ] Jest configured with React Native preset
- [ ] React Native Testing Library installed
- [ ] Test utilities and helpers directory created
- [ ] Sample test file created and passing
- [ ] `npm test` command runs successfully
- [ ] Test coverage reporting configured
- [ ] Mock setup for Expo modules
- [ ] CI/CD can run tests

### Technical Implementation Notes

**Testing Dependencies** (partially installed in Story 0.4):

```bash
npm install --save-dev jest @testing-library/react-native @testing-library/jest-native
npm install --save-dev @types/jest
npm install --save-dev jest-expo
```

**Jest Configuration** (jest.config.js):

```javascript
module.exports = {
  preset: 'jest-expo',
  setupFilesAfterEnv: ['<rootDir>/src/__tests__/setup.ts'],
  transformIgnorePatterns: [
    'node_modules/(?!((jest-)?react-native|@react-native(-community)?)|expo(nent)?|@expo(nent)?/.*|@expo-google-fonts/.*|react-navigation|@react-navigation/.*|@unimodules/.*|unimodules|sentry-expo|native-base|react-native-svg)',
  ],
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.styles.ts',
    '!src/**/*.test.{ts,tsx}',
    '!src/__tests__/**',
  ],
  coverageThreshold: {
    global: {
      statements: 60,
      branches: 50,
      functions: 60,
      lines: 60,
    },
  },
  moduleNameMapper: {
    '^@/(.*)$': '<rootDir>/src/$1',
    '^@components/(.*)$': '<rootDir>/src/components/$1',
    '^@screens/(.*)$': '<rootDir>/src/screens/$1',
    '^@services/(.*)$': '<rootDir>/src/services/$1',
    '^@hooks/(.*)$': '<rootDir>/src/hooks/$1',
    '^@models/(.*)$': '<rootDir>/src/models/$1',
    '^@utils/(.*)$': '<rootDir>/src/utils/$1',
  },
};
```

**Test Setup File** (src/**tests**/setup.ts):

```typescript
import '@testing-library/jest-native/extend-expect';

// Mock Expo modules
jest.mock('expo-secure-store');
jest.mock('expo-camera');
jest.mock('expo-av');
jest.mock('expo-media-library');
jest.mock('expo-file-system');
jest.mock('expo-web-browser');

// Mock AsyncStorage
jest.mock('@react-native-async-storage/async-storage', () =>
  require('@react-native-async-storage/async-storage/jest/async-storage-mock')
);

// Silence console warnings in tests
global.console = {
  ...console,
  error: jest.fn(),
  warn: jest.fn(),
};
```

**Test Utilities** (src/**tests**/helpers/testUtils.tsx):

```typescript
import React from 'react';
import { render, RenderOptions } from '@testing-library/react-native';
import { NavigationContainer } from '@react-navigation/native';

// Custom render function that includes providers
const AllTheProviders = ({ children }: { children: React.ReactNode }) => {
  return (
    <NavigationContainer>
      {children}
    </NavigationContainer>
  );
};

const customRender = (ui: React.ReactElement, options?: RenderOptions) =>
  render(ui, { wrapper: AllTheProviders, ...options });

// Re-export everything
export * from '@testing-library/react-native';
export { customRender as render };
```

**Mock Helpers** (src/**tests**/mocks/index.ts):

```typescript
// Mock user data
export const mockUser = {
  id: 'test-user-id',
  email: 'test@example.com',
  username: 'testuser',
  createdAt: new Date('2025-01-01'),
  stats: {
    totalVideos: 10,
    totalHighlights: 5,
    totalViews: 100,
  },
};

// Mock video data
export const mockVideo = {
  id: 'test-video-id',
  userId: 'test-user-id',
  localUri: 'file:///test/video.mp4',
  thumbnailUri: 'file:///test/thumb.jpg',
  duration: 15,
  resolution: '720p' as const,
  type: 'commentary' as const,
  createdAt: new Date('2025-01-15'),
  views: 50,
  metadata: {
    deviceModel: 'iPhone 13',
    osVersion: '17.0',
    appVersion: '1.0.0',
    recordingMode: 'front' as const,
  },
};
```

**Sample Test File** (src/components/common/Button/Button.test.tsx):

```typescript
import React from 'react';
import { fireEvent } from '@testing-library/react-native';
import { render } from '@/__tests__/helpers/testUtils';

// Placeholder Button component
const Button = ({ title, onPress }: { title: string; onPress: () => void }) => (
  <button onClick={onPress}>{title}</button>
);

describe('Button Component', () => {
  it('renders correctly with title', () => {
    const { getByText } = render(<Button title="Press Me" onPress={() => {}} />);
    expect(getByText('Press Me')).toBeTruthy();
  });

  it('calls onPress when pressed', () => {
    const mockOnPress = jest.fn();
    const { getByText } = render(<Button title="Press Me" onPress={mockOnPress} />);

    fireEvent.press(getByText('Press Me'));
    expect(mockOnPress).toHaveBeenCalledTimes(1);
  });
});
```

**Package.json Scripts:**

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "test:ci": "jest --ci --coverage --maxWorkers=2"
  }
}
```

### Verification Steps

1. Run `npm test` - sample test should pass
2. Run `npm run test:coverage` - should show coverage report
3. Verify test output shows "1 passed, 1 total"
4. Check coverage/lcov-report/index.html for visual report

### Definition of Done

- [ ] Jest configuration complete
- [ ] Test setup file created
- [ ] Test utilities and mocks created
- [ ] Sample test passes
- [ ] Coverage reporting works
- [ ] Documentation updated
- [ ] Code reviewed and merged

### Blockers / Dependencies

- **Requires**: Story 0.1 (project), Story 0.4 (dependencies)

### Notes

- Coverage threshold: 60% (Architecture Section 11.5)
- Detox (E2E testing) will be added in Epic 4 (Polish phase)
- Mock all Expo modules to avoid native module errors in tests

---

## Story 0.6: Set Up CI/CD Pipeline

### Story Metadata

```yaml
id: story-0.6
title: Configure GitHub Actions CI/CD Pipeline
epic: Epic 0 - Project Foundation
priority: P1
estimated_effort: 2-3 hours
dependencies: [story-0.2, story-0.5]
assignee: Tech Lead
status: Ready
```

### User Story

**As a** developer  
**I want** automated CI/CD running on every commit  
**So that** we catch errors early and maintain code quality

### Context

Architecture Section 12.3 defines the CI/CD pipeline using GitHub Actions. We need automated linting, testing, and builds on every push/PR.

### Acceptance Criteria

- [ ] GitHub Actions workflow file created
- [ ] Workflow runs on push to main and develop branches
- [ ] Workflow runs on all pull requests
- [ ] Linting executes automatically
- [ ] Tests execute automatically
- [ ] Test coverage uploaded to Codecov
- [ ] Build success/failure visible in PR checks
- [ ] Badge in README shows build status

### Technical Implementation Notes

**GitHub Actions Workflow** (.github/workflows/ci.yml):

```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  lint-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run linter
        run: npm run lint

      - name: Run tests
        run: npm run test:ci

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage/lcov.info
          fail_ci_if_error: false

  build-check:
    runs-on: ubuntu-latest
    needs: lint-and-test
    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Check TypeScript
        run: npx tsc --noEmit

      - name: Verify build
        run: npm run build --if-present || echo "No build script defined yet"
```

**README Badge:**

```markdown
# GameDuel

[![CI](https://github.com/[your-username]/gameduel/actions/workflows/ci.yml/badge.svg)](https://github.com/[your-username]/gameduel/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/[your-username]/gameduel/branch/main/graph/badge.svg)](https://codecov.io/gh/[your-username]/gameduel)

[Rest of README...]
```

**Branch Protection Rules** (Configure in GitHub Settings):

- Require PR reviews: 1
- Require status checks to pass:
  - `lint-and-test`
  - `build-check`
- Require branches to be up to date
- Dismiss stale PR approvals

### Verification Steps

1. Create a new branch with intentional lint error
2. Push and create PR
3. Verify CI runs and fails
4. Fix error, push again
5. Verify CI passes
6. Check Codecov report

### Definition of Done

- [ ] GitHub Actions workflow created
- [ ] CI runs successfully on clean code
- [ ] CI fails on linting errors
- [ ] CI fails on test failures
- [ ] Coverage reporting works
- [ ] Branch protection rules configured
- [ ] README badge added
- [ ] Documentation updated

### Blockers / Dependencies

- **Requires**: Story 0.2 (linting), Story 0.5 (tests)
- **Requires**: GitHub repository

### Notes

- Codecov account needed for coverage reporting
- CI must pass before merging to main
- Builds for iOS/Android will be added in Epic 4

---

## Story 0.7: Create Project Documentation

### Story Metadata

```yaml
id: story-0.7
title: Create Developer Documentation and README
epic: Epic 0 - Project Foundation
priority: P2
estimated_effort: 2-3 hours
dependencies: [story-0.1, story-0.2, story-0.3, story-0.4, story-0.5, story-0.6]
assignee: Tech Lead
status: Ready
```

### User Story

**As a** new developer joining the project  
**I want** comprehensive setup documentation  
**So that** I can get started quickly without confusion

### Context

We need clear documentation for developers to understand the project structure, setup process, and development workflow.

### Acceptance Criteria

- [ ] README.md contains comprehensive setup instructions
- [ ] CONTRIBUTING.md created with development guidelines
- [ ] docs/ARCHITECTURE.md created (summary with link to full doc)
- [ ] docs/DEVELOPMENT.md created with workflow guide
- [ ] All documentation is clear and tested by fresh setup
- [ ] Links to PRD and Architecture documents included
- [ ] Troubleshooting section included

### Technical Implementation Notes

**README.md Structure:**

```markdown
# GameDuel

[![CI](https://github.com/[username]/gameduel/actions/workflows/ci.yml/badge.svg)](https://github.com/[username]/gameduel/actions/workflows/ci.yml)

> Your Gaming Moments, Plus Context

GameDuel is a mobile app that empowers gaming enthusiasts to create 15-second pre/post-match commentary videos enriched with gaming data from Steam, Xbox Live, and PlayStation Network.

## 🚀 Quick Start

### Prerequisites

- Node.js 18+
- npm or yarn
- Expo CLI: `npm install -g expo-cli`
- iOS Simulator (Mac) or Android Emulator

### Installation

\`\`\`bash

# Clone the repository

git clone https://github.com/[username]/gameduel.git
cd gameduel

# Install dependencies

npm install

# Start development server

npm start
\`\`\`

Press `i` for iOS simulator or `a` for Android emulator.

## 📁 Project Structure

\`\`\`
gameduel/
├── src/
│ ├── screens/ # Screen components
│ ├── components/ # Reusable components
│ ├── navigation/ # Navigation setup
│ ├── services/ # Business logic
│ ├── models/ # TypeScript types
│ └── ...
├── assets/ # Images, icons, fonts
├── docs/ # Documentation
└── README.md
\`\`\`

See [Directory Structure](./docs/ARCHITECTURE.md) for details.

## 🛠️ Development

### Available Scripts

- `npm start` - Start Expo dev server
- `npm run lint` - Run ESLint
- `npm run format` - Format code with Prettier
- `npm test` - Run tests
- `npm run test:coverage` - Generate coverage report

### Code Quality

This project uses:

- **ESLint** for code linting
- **Prettier** for code formatting
- **Husky** for git hooks
- **Jest** for testing

Pre-commit hooks ensure code quality before commits.

## 📚 Documentation

- [Architecture Overview](./docs/ARCHITECTURE.md)
- [Development Workflow](./docs/DEVELOPMENT.md)
- [Contributing Guidelines](./CONTRIBUTING.md)
- [Full Architecture Document](./docs/GameDuel-Architecture.md)
- [Product Requirements (PRD)](./docs/GameDuel-PRD.md)

## 🧪 Testing

\`\`\`bash

# Run all tests

npm test

# Watch mode

npm run test:watch

# Coverage report

npm run test:coverage
\`\`\`

## 🔧 Troubleshooting

### Common Issues

**"Metro bundler not starting"**
\`\`\`bash
npm start -- --reset-cache
\`\`\`

**"Dependency errors after npm install"**
\`\`\`bash
rm -rf node_modules package-lock.json
npm install
\`\`\`

**"Expo CLI not found"**
\`\`\`bash
npm install -g expo-cli
\`\`\`

## 📄 License

[License Type] - See LICENSE file for details

## 🤝 Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for development guidelines.

## 📧 Contact

- Product Manager: [email]
- Tech Lead: [email]
```

**CONTRIBUTING.md:**

```markdown
# Contributing to GameDuel

## Development Workflow

1. **Create a feature branch**
   \`\`\`bash
   git checkout -b feature/your-feature-name
   \`\`\`

2. **Make your changes**
   - Follow code style guidelines
   - Write tests for new features
   - Update documentation as needed

3. **Run checks locally**
   \`\`\`bash
   npm run lint
   npm test
   \`\`\`

4. **Commit your changes**
   \`\`\`bash
   git commit -m "feat: add new feature"
   \`\`\`

   **Commit Message Format:**
   - `feat:` New feature
   - `fix:` Bug fix
   - `docs:` Documentation only
   - `style:` Code style (formatting, etc.)
   - `refactor:` Code refactoring
   - `test:` Adding tests
   - `chore:` Maintenance tasks

5. **Push and create PR**
   \`\`\`bash
   git push origin feature/your-feature-name
   \`\`\`

## Code Style

- Follow ESLint rules
- Use Prettier for formatting
- Write meaningful variable names
- Add JSDoc comments for functions
- Keep functions small and focused

## Testing

- Write unit tests for utilities and services
- Write component tests for UI components
- Aim for 60%+ code coverage
- Mock external dependencies

## Pull Request Process

1. Ensure CI passes
2. Get code review from at least 1 developer
3. Address review comments
4. Squash commits if needed
5. Merge when approved

## Questions?

Contact the Tech Lead or post in the team channel.
```

**docs/DEVELOPMENT.md:**

```markdown
# Development Workflow

## Daily Development

### Starting Work

1. Pull latest changes: `git pull origin develop`
2. Create feature branch: `git checkout -b feature/story-X.X`
3. Start dev server: `npm start`

### During Development

- Run linter frequently: `npm run lint`
- Write tests alongside code
- Commit often with clear messages

### Before Committing

- Run full test suite: `npm test`
- Verify linting: `npm run lint`
- Check formatting: `npm run format:check`

Pre-commit hooks will run automatically.

## Story Development Process

Follow the BMAD method:

1. Read story file thoroughly
2. Implement acceptance criteria
3. Write tests
4. Update documentation
5. Create PR
6. Address review comments
7. Merge when approved

## Environment Setup

### Required Tools

- Node.js 18+
- Expo CLI
- Xcode (for iOS development)
- Android Studio (for Android development)

### Optional Tools

- React Native Debugger
- Reactotron
- VS Code with extensions:
  - ESLint
  - Prettier
  - React Native Tools

## Debugging

### React Native Debugger

1. Install: `brew install --cask react-native-debugger`
2. Open before starting Expo
3. Shake device/simulator to open debug menu
4. Select "Debug with Chrome"

### Console Logging

- Use `console.log` for development
- Use `console.warn` for warnings
- Use `console.error` for errors
- Remove logs before committing

## Common Workflows

### Adding a New Component

1. Create folder: `src/components/[category]/[ComponentName]/`
2. Create files:
   - `[ComponentName].tsx`
   - `[ComponentName].styles.ts`
   - `[ComponentName].test.tsx`
3. Export from `index.ts`
4. Write tests
5. Use component in screen

### Adding a New Screen

1. Create folder: `src/screens/[screen-name]/`
2. Create screen component
3. Add to navigation
4. Write tests
5. Connect to context/hooks

### Adding a New Service

1. Create: `src/services/[service-name]/[ServiceName].ts`
2. Define interface
3. Implement business logic
4. Write unit tests
5. Use via dependency injection

## Best Practices

- **Component Size**: Keep components under 200 lines
- **Function Size**: Keep functions under 20 lines
- **File Organization**: One component per file
- **Imports**: Use path aliases (`@/` instead of `../../`)
- **State Management**: Use Context for global state
- **Props**: Always define TypeScript interfaces
- **Styles**: Keep styles in separate `.styles.ts` files

## Getting Help

- Check Architecture document first
- Review similar existing code
- Ask in team channel
- Schedule pairing session if stuck
```

### Verification Steps

1. Have new developer follow README setup
2. Verify all links work
3. Test troubleshooting steps
4. Confirm documentation completeness

### Definition of Done

- [ ] README.md complete
- [ ] CONTRIBUTING.md created
- [ ] DEVELOPMENT.md created
- [ ] All links tested
- [ ] Fresh setup tested
- [ ] Code reviewed and merged

### Blockers / Dependencies

- **Requires**: All previous stories (documentation reflects final setup)

### Notes

- Keep documentation up-to-date as project evolves
- Link to full Architecture document (not duplicate content)
- Use clear, beginner-friendly language

---

## Epic 0 Summary

### Total Estimated Effort

**8-10 days** (1-2 weeks)

### Story Breakdown

1. Story 0.1: Initialize Project - 2-4 hours
2. Story 0.2: Configure Code Quality - 3-4 hours
3. Story 0.3: Directory Structure - 2-3 hours
4. Story 0.4: Install Dependencies - 2-3 hours
5. Story 0.5: Testing Infrastructure - 3-4 hours
6. Story 0.6: CI/CD Pipeline - 2-3 hours
7. Story 0.7: Documentation - 2-3 hours

### Dependencies Flow

```
0.1 (Initialize)
  ├─> 0.2 (Code Quality)
  ├─> 0.3 (Directory)
  └─> 0.4 (Dependencies)
        └─> 0.5 (Testing)
              └─> 0.6 (CI/CD)
                    └─> 0.7 (Documentation)
```

### Success Criteria Checklist

- [ ] Project builds successfully
- [ ] All developers can run locally
- [ ] Linting and formatting automated
- [ ] Tests run successfully
- [ ] CI/CD pipeline working
- [ ] Directory structure matches architecture
- [ ] Documentation complete

### Post-Epic Deliverables

- ✅ Fully configured Expo + TypeScript project
- ✅ Code quality tools operational
- ✅ Testing infrastructure ready
- ✅ CI/CD pipeline functional
- ✅ Clear documentation for team
- ✅ Foundation ready for Epic 1 (User Management)

---

## Handoff to Epic 1

Once Epic 0 is complete, the team is ready to begin **Epic 1: User Management** (Authentication & Profile).

**Epic 1 Prerequisites** (all met after Epic 0):

- ✅ Project initialized
- ✅ Development environment ready
- ✅ Testing framework available
- ✅ CI/CD operational
- ✅ Team onboarded

**Next Epic**: Epic 1 - User Management (Authentication, Profile, Settings)

---

**Epic 0 Status**: ✅ Ready for Development  
**Last Updated**: 2025-10-23  
**Epic Owner**: Tech Lead
