# CLAUDE.md - Project Rules & Guidelines

This file contains project-specific rules and conventions that Claude should always follow when working on this codebase.

## Project planning method

- I will discuss my plan using the draft.md file. This will just be a mind dump of the concepts.
- If there are any further discussions or questions needed to clarify the concepts discussed, you can add them to questions.md. I will then copy and past this to draft.md and answer and discuss the questions etc.
- We will itterate like this an then build up the projectSpecs.md file to be the final source of truth for the project.

NOTE: We are NOT building anything yet. ONLY PLANNING

<!--
## Project Overview

- **Framework**: React 18 + TypeScript + Vite
- **AWS Services**: Amplify, Cognito, AppSync, DynamoDB
- **UI Library**: Material-UI (MUI) v7
- **Routing**: React Router v7
- **Styling**: Emotion (CSS-in-JS)

## Development Commands

- **Dev Server**: `npm run dev`
- **Build**: `npm run build` (includes TypeScript compilation)
- **Lint**: `npm run lint`
- **Preview**: `npm run preview`

## Code Style & Conventions

### TypeScript

- Always use TypeScript for new components and files
- Prefer explicit typing over `any`
- Use proper interface definitions for props and state

### React Components

- Use functional components with hooks
- Follow Material-UI design patterns
- Use proper prop typing with TypeScript interfaces
- Prefer arrow function components for consistency

### File Organization

- Components should be in appropriate directories
- Follow existing import patterns
- Use absolute imports where configured

### AWS Amplify Integration

- Follow Amplify best practices for authentication
- Use proper error handling for AWS service calls
- Respect AWS service quotas and limits
- Always handle loading and error states

### Security

- Never commit AWS credentials or secrets
- Use environment variables for configuration
- Follow AWS security best practices
- Validate user inputs properly

## Testing & Quality

- Run `npm run lint` before committing changes
- Ensure TypeScript compilation passes with `npm run build`
- Test authentication flows thoroughly
- Verify AWS service integrations work correctly

## Git Workflow

- Use descriptive commit messages
- Keep commits focused and atomic
- Test builds before pushing changes

## Performance Guidelines

- Optimize bundle size where possible
- Use React.memo() for expensive components
- Implement proper loading states
- Consider AWS service costs in implementation decisions

## Documentation

- Update this file when adding new conventions
- Document complex AWS service integrations
- Include setup instructions for new team members
- Keep README.md updated with deployment information

## Common Patterns to Follow

- Use MUI theming system consistently
- Implement proper error boundaries
- Follow React Router v7 patterns for navigation
- MUI components takes preference - But use Amplify UI components when really needed
- Implement responsive design with MUI breakpoints

---

_This file should be updated as the project evolves and new conventions are established._
-->
