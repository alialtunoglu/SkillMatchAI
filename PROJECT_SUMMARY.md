# SkillMatchAI - Project Summary

## 📋 Overview

**SkillMatchAI** (Micro Learning Plan Platform) is a micro-learning platform that helps users create and track personalized learning plans. The platform personalizes the learning experience with **AI-powered** content generation and uses adaptive learning methods.

## 🎯 Core Purpose

This platform enables users to:
- Define their own learning goals
- Plan the daily time they can dedicate
- Receive customized content according to their learning styles (visual, auditory, practical, reading)
- Follow a modular and progressive learning path
- Track and evaluate their progress

## 🤖 LLM (Large Language Model) Usage

### ✅ YES, LLM is Used

The project extensively uses **Google Gemini AI** models:

#### Models Used:
1. **Gemini 2.5 Flash** - Primary model (for fast responses)
2. **Gemini 2.5 Pro** - Backup model (if flash fails)
3. **Gemini 1.5 Flash** - For content generation

#### LLM Use Cases:

##### 1. **Learning Plan Generation** (`/api/generate-plan`)
- Generates personalized learning plans based on user goals
- Customized according to number of modules, difficulty level, and learning style
- Example: "I want to learn Python, I have 4 weeks" → AI creates a complete training program

##### 2. **Module Content Generation** (`/api/generate-module-content`)
AI generates content in 4 different sections for each module:

- **Introduction and Core Concepts**: AI prepares an introduction to teach the topic from scratch
- **Detailed Explanations**: Historical development, methodologies, examples, and video suggestions
- **Practical Tasks**: Hands-on tasks, step-by-step instructions, and completion criteria
- **Summary and Evaluation**: Comprehensive summary, assessment questions, and performance indicators

##### 3. **Student Evaluation** (`/api/evaluate-student-progress`)
- Analyzes student responses
- Determines understanding level (1-5 scale)
- Identifies strengths and weaknesses
- Adaptively adjusts the difficulty level of the next module (easier/same/harder)
- Provides detailed feedback and recommendations

#### Technical Details:
```typescript
// Example AI Call
const { text } = await generateText({
  model: google('gemini-2.5-flash'),
  prompt: prompt,
  maxOutputTokens: 8192,
  temperature: 0.0-0.7, // Low temperature for consistency
  topP: 0.1
});
```

## 🔍 RAG (Retrieval-Augmented Generation) Usage

### ❌ NO, RAG is Not Used

The project currently **does not use RAG (Retrieval-Augmented Generation)** technology.

#### What is RAG?
RAG is a technique that enables large language models to retrieve relevant information from knowledge bases (vector databases) to generate more accurate and up-to-date answers.

#### Why RAG is Not in the Project:
1. **Direct LLM Usage**: Content is generated directly from Gemini model's own knowledge
2. **No Vector Database**: No use of vector databases like Pinecone, Weaviate, or Qdrant
3. **No Embedding Process**: No text embedding or similarity search is performed
4. **No External Knowledge Source**: The model doesn't fetch data from external sources

#### Can RAG Be Added?
Yes, RAG could be added in the future:
- Educational materials could be uploaded to a vector database
- Relevant documents could be retrieved for user questions and provided as context to the LLM
- Video content, articles, and source documents could be indexed
- This would enable more current and specific information generation

## 🛠️ Technology Stack

### Frontend:
- **Next.js 15.2.4** (React 19)
- **TypeScript**
- **Tailwind CSS** - Styling
- **Radix UI** - UI components
- **Lucide React & React Icons** - Icons

### Backend & AI:
- **Next.js API Routes** - Backend API
- **Supabase** - Database and Authentication
- **Google Gemini AI** (`@ai-sdk/google`, `@google/generative-ai`)
- **Vercel AI SDK** (`ai` package)

### Database (Supabase):
- `users` - User information
- `learning_plans` - Learning plans
- `modules` - Modules
- `module_contents` - AI-generated contents
- `student_progress` - Student progress
- `practical_tasks` - Practical tasks
- `task_submissions` - Task submissions

## 🎓 Core Features

### 1. **Personalized Learning**
- Learning goal definition
- Daily time planning (15 min, 30 min, 1 hour, 2 hours)
- Duration selection (2, 4, 8, 12 weeks)
- Learning style (visual, auditory, practical, reading)
- Target level (beginner, intermediate, advanced)

### 2. **AI-Powered Content Generation**
- Original content for each module
- Materials suited to learning style
- Video suggestions and resources
- Interactive tasks

### 3. **Adaptive Learning**
- Difficulty adjustment based on student performance
- Identification of strengths/weaknesses
- Personalized feedback
- Next module recommendations

### 4. **Modular Structure**
- Progressively advancing modules
- Quiz and exam modules
- Module completion tracking
- Progress indicators

### 5. **User Management**
- Supabase Authentication
- User profiles
- Multiple plan support
- Plan active/inactive status

## 📊 Data Flow

```
User → Create Plan → Gemini AI → Personalized Plan → Supabase

Select Module → Generate Content → Gemini AI → 4 Section Content → Supabase

Evaluation → Answers → Gemini AI → Performance Analysis → Adaptive Adjustment
```

## 🚀 Highlights

1. **Full AI Integration**: Not just simple templates, but unique content for each user
2. **Adaptive System**: Dynamic adjustment based on student performance
3. **Comprehensive Evaluation**: Detailed analysis and feedback with AI
4. **Multi-faceted Content**: Text, video suggestions, practical tasks, assessments
5. **Modern Stack**: Current technologies with Next.js 15, React 19, TypeScript

## 📈 Future Development Opportunities

### For Adding RAG:
1. **Vector Database Integration** (e.g., Pinecone, Supabase Vector)
2. **Educational Material Indexing**: YouTube videos, articles, e-books
3. **Semantic Search**: Finding the most suitable sources for user questions
4. **Citation/Source Attribution**: Including sources in generated content
5. **Current Information**: Including news and current developments in content generation

### Other Improvements:
- Multi-language support
- Video content generation
- Voice assistant
- Social learning features
- Gamification (badges, leaderboard)

## 🔐 Security and Rate Limiting

- **Authentication**: Secure user management with Supabase Auth
- **Rate Limiting**: IP-based rate limiting (e.g., 5 requests/minute)
- **Token Verification**: JWT token check on every API call
- **Authorization**: Users can only access their own plans

## 📝 Conclusion

**SkillMatchAI** offers a personalized, adaptive micro-learning platform using Google Gemini AI models. **LLM usage is extensive** in plan creation, content generation, and evaluation phases. However, **RAG technology is not currently used** - all content is generated from the LLM's own knowledge. In the future, with RAG integration, more current and source-based content generation could become possible.

---

**Developer**: Ali Altunoğlu  
**Platform**: Next.js + Supabase + Google Gemini AI  
**Deployment**: Vercel  
**License**: Private
