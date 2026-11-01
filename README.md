# AI Mock Interview Platform

An AI-powered mock interview application built as a learning project to explore how generative AI, voice interfaces, authentication, and cloud data storage can work together.

The application lets a user prepare for a role-specific interview, answer questions through a voice-based interview experience, and review AI-generated feedback from the interview transcript.

> **Project note:** This repository started from the open-source Prepwise / AI Mock Interviews project by JavaScript Mastery. I used that codebase as a learning foundation and am working to understand, document, and improve the application. The original project and tutorial are credited below. Please distinguish the existing starter implementation from any changes I have personally made.

## Project overview

Preparing for interviews takes practice, but it can be difficult to get repeated interview experience and structured feedback. This project explores a way to practise in a simulated interview environment and receive an initial review of responses.

### Main workflow

1. The user signs up or signs in.
2. The user provides interview details such as the target role, experience level, technology stack, interview type, and number of questions.
3. Google Gemini is used to generate interview questions based on those details.
4. A Vapi voice assistant conducts the interview and captures the conversation transcript.
5. The transcript is sent for AI-generated feedback.
6. The user can review the interview and feedback through the application dashboard.

## Features in the current implementation

- **Authentication:** Email and password sign-up and sign-in using Firebase Authentication.
- **Interview question generation:** Generates role- and technology-focused questions using Google Gemini.
- **Voice-based interview:** Uses Vapi to provide a conversational interview experience.
- **AI feedback:** Analyses the interview transcript and returns an overall assessment, category scores, strengths, and areas for improvement.
- **Feedback categories:** Communication Skills, Technical Knowledge, Problem-Solving, Cultural & Role Fit, and Confidence & Clarity.
- **Interview dashboard:** Displays interview records and available feedback.
- **Responsive interface:** Built with reusable UI components and Tailwind CSS.

*The feedback is AI-generated and should be treated as practice guidance, not as a definitive assessment of a candidate's ability or a guarantee of interview performance.*

## Technology stack

| Technology | Purpose |
| --- | --- |
| Next.js | Application framework and server-side functionality |
| React | User interface |
| TypeScript | Application code and type safety |
| Firebase Authentication | User authentication |
| Firebase / Firestore | Interview and feedback data storage |
| Google Gemini | Interview question generation and transcript feedback |
| Vapi | Voice-based interview experience |
| Tailwind CSS | Styling |
| shadcn/ui | UI components |
| Zod | Input validation |

### Important AI integration detail

Gemini and Vapi have different responsibilities in this application:

- **Google Gemini** is used for generating interview questions and analysing the completed interview transcript.
- **Vapi** manages the voice-interview experience. The voice assistant configuration uses separate speech and language services, so the voice conversation should not be described as being powered entirely by Gemini.

## Feedback approach

The feedback-generation prompt asks the model to assess the interview transcript across five categories:

1. Communication Skills
2. Technical Knowledge
3. Problem-Solving
4. Cultural & Role Fit
5. Confidence & Clarity

Each category is requested as a score out of 100 with a written comment. The feedback also includes an overall assessment, strengths, and areas for improvement.

Because this is an AI-generated evaluation, scores can vary between attempts and may not always be fully consistent. A useful next improvement is to validate the response structure and score ranges, and to make feedback more evidence-based by connecting comments to specific answers in the transcript.

## Getting started

### Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended)
- npm
- [Git](https://git-scm.com/)
- Firebase project
- Vapi account and configured assistant/workflow
- Google AI Studio API key for Gemini

### 1. Clone this repository

```bash
git clone https://github.com/dubey-7/ai_mock_interview.git
cd ai_mock_interview
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env.local` file in the project root. Add the variables used by the application and provide your own credentials:

```env
NEXT_PUBLIC_VAPI_WEB_TOKEN=
NEXT_PUBLIC_VAPI_WORKFLOW_ID=

GOOGLE_GENERATIVE_AI_API_KEY=

NEXT_PUBLIC_BASE_URL=

NEXT_PUBLIC_FIREBASE_API_KEY=
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=
NEXT_PUBLIC_FIREBASE_PROJECT_ID=
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=
NEXT_PUBLIC_FIREBASE_APP_ID=

FIREBASE_PROJECT_ID=
FIREBASE_CLIENT_EMAIL=
FIREBASE_PRIVATE_KEY=
```

Use the Firebase configuration from your Firebase project, the Vapi values from your Vapi dashboard, and a Gemini API key from Google AI Studio. Keep private credentials out of source control. Never commit your real `.env.local` file or expose service-account credentials in client-side code.

### 4. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Areas for improvement

The following are improvement opportunities identified while reviewing the codebase. They should not be interpreted as features that are already implemented:

- Add server-side authentication and authorization checks to protect interview and feedback records.
- Validate interview-generation inputs and AI responses with schemas before saving or displaying them.
- Enforce score boundaries and a consistent feedback response structure.
- Improve error handling for failed AI requests, malformed model responses, and voice-session interruptions.
- Make feedback more actionable by linking comments to specific transcript answers and suggesting concrete ways to improve.
- Add progress tracking across multiple interview attempts.
- Add tests for authentication, question generation, feedback processing, and access control.

## Learning outcomes

This project provides practical exposure to:

- Integrating generative AI APIs into a web application.
- Building a voice-based user interaction flow.
- Working with authentication and cloud data storage.
- Passing interview transcripts through an AI feedback workflow.
- Structuring a full-stack application with reusable components.
- Reviewing AI-generated outputs for reliability, validation, and user experience.

## Credits and references

This project was developed using the open-source **AI Mock Interviews / Prepwise** project by [Adrian Hajdin and JavaScript Mastery](https://github.com/adrianhajdin/ai_mock_interviews) as its starting point.

- Original repository: [JavaScript Mastery – AI Mock Interviews](https://github.com/adrianhajdin/ai_mock_interviews)
- Tutorial: [JavaScript Mastery on YouTube](https://www.youtube.com/watch?v=8GK8R77Bd7g)

The original authors retain credit for their starter implementation and tutorial. This repository is maintained as a learning project, with changes and improvements documented as they are made. Refer to the original repository's license before redistributing or reusing its code.
