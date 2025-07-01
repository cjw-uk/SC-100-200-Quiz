# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-page Microsoft Security Certification Quiz Engine built as a standalone HTML application. It provides interactive quiz functionality for SC-100 (Cybersecurity Architect) and SC-200 (Security Operations Analyst) certification preparation.

## Architecture

### Single-File Application
- **File**: `index.html` - Contains HTML structure, CSS styling, JavaScript logic, and embedded question bank
- **Architecture Pattern**: Vanilla JavaScript SPA with state management through global variables
- **No Build Process**: Direct browser execution, no compilation or bundling required

### Core Components

**Application State Management**:
- Global variables manage quiz state (`currentExam`, `selectedObjectives`, `quizQuestions`, `userAnswers`)
- State transitions: Setup → Quiz → Results → Setup (cyclical)

**Question Bank Structure**:
- Organized by exam type (`SC-100`, `SC-200`)
- Each exam contains `objectives` array and `questions` array
- Questions include: objective mapping, difficulty level, scenario text, multiple choice options, correct answers, explanations, and Microsoft Learn links

**UI Flow**:
1. **Setup Screen**: Exam selection, objective filtering, question count configuration
2. **Quiz Screen**: Question display, progress tracking, answer submission, navigation
3. **Results Screen**: Score calculation, objective breakdown, study recommendations

### Key Functions

**Quiz Management**:
- `startQuiz()` - Initializes quiz with filtered questions based on selected objectives
- `displayQuestion()` - Renders current question with proper input types (radio/checkbox)
- `submitAnswer()` - Validates and stores user response, shows explanation
- `finishQuiz()` - Calculates results and transitions to results screen

**Navigation**:
- `previousQuestion()` / `nextQuestion()` - Question navigation with state preservation
- `updateNavigationButtons()` - Dynamic button state management

**Scoring**:
- `calculateResults()` - Computes overall and per-objective scores
- `generateStudyRecommendations()` - Creates targeted study suggestions based on performance

## Development Commands

Since this is a standalone HTML file with no build system:

**Local Development**:
```bash
# Serve locally (Python 3)
python -m http.server 8000

# Serve locally (Python 2)
python -m SimpleHTTPServer 8000

# Or use any local server of choice
```

**Testing**:
- Manual testing in browser required
- No automated test framework present
- Test across different browsers for compatibility

## Content Management

**Adding Questions**:
- Questions are embedded in the `questionBank` JavaScript object
- Follow existing question structure with required fields: `objective`, `difficulty`, `question`, `options`, `correct`, `explanation`, `learnMore`
- Support for both single and multiple-choice questions based on `correct` array length

**Exam Configuration**:
- Objectives defined in `questionBank[exam].objectives`
- Questions mapped to objectives via zero-based index
- Difficulty levels: `beginner`, `intermediate`, `advanced`

## Browser Compatibility

- Uses modern JavaScript features (const/let, arrow functions, array methods)
- CSS Grid and Flexbox for responsive layout
- Targets modern browsers (ES6+)
- No external dependencies or frameworks