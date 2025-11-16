# CS Career Advisor Chatbot

A conversational agent built in the Pandorabots platform using AIML that helps computer science students explore which computing careers fit their strengths, interests, and work preferences.

The bot acts like a lightweight career advisor: it asks targeted questions, remembers answers, and then recommends one or more roles with a brief explanation of why they match the student.

---

## Scenario and Goals

Universities are graduating more computer science students every year, and it is not realistic for a human advisor to meet with everyone individually. This chatbot was designed to:

- Talk with students who are **about to graduate**.
- Ask about their **technical strengths**, **preferred work style**, and **interests**.
- Recommend **five specific computing job types** that typically require a CS degree.
- Give **short explanations** of why each role matches the student’s profile.
- Reduce advisor workload while still giving students meaningful, personalized guidance.

---

## Career Paths Covered

The chatbot focuses on five concrete job types that commonly require an undergraduate degree in computer science:

1. **DevOps Engineer**  
   - For students who enjoy automation, scripting, CI/CD pipelines, and improving how software is deployed and monitored.

2. **Vulnerability Researcher (Security Researcher)**  
   - For students who like digging into low-level behavior, reverse engineering, and security testing.

3. **Cloud Consultant / Cloud Solutions Engineer**  
   - For students interested in cloud platforms, architecture, and helping organizations design scalable solutions.

4. **Computer Network Architect**  
   - For students who enjoy networking, infrastructure, protocols, and designing complex network topologies.

5. **Data Scientist**  
   - For students who are drawn to statistics, machine learning, data storytelling, and using data to drive decisions.

The bot steers the conversation toward one or more of these paths based on the student’s answers.

---

## Core Chatbot Functionality

### 1. Greeting and Onboarding

- Welcomes the student and explains its purpose.
- Asks what stage they are in:
  - About to graduate
  - Early in their program
  - Just exploring options
- If the student is **not** close to graduation, the bot still offers general information about roles but frames advice more broadly.

### 2. Preference Gathering

Through a series of questions, the bot probes areas such as:

- **What you enjoy doing:**
  - Building systems end-to-end
  - Breaking things and finding weaknesses
  - Designing infrastructure and networks
  - Working with data and models
  - Helping clients solve technical problems

- **Comfort with different topics:**
  - Operating systems, scripting, and automation
  - Security and exploit analysis
  - Networking concepts and protocols
  - Probability, statistics, and machine learning
  - Cloud platforms and architecture

- **Work-style preferences:**
  - Hands-on building vs. analysis
  - Working with cross-functional teams vs. individual research
  - Working directly with clients vs. working mostly behind the scenes

The bot uses simple internal “rules” (implemented in AIML patterns and templates) to track which career paths the student seems aligned with.

### 3. Career Recommendation Logic

- The bot maps answers to **flags** for each of the five careers.  
  For example:
  - Strong interest in automation + systems + cloud → DevOps / Cloud Consultant.
  - Security / reverse engineering + “enjoy breaking things” → Vulnerability Researcher.
  - Interest in networks + infrastructure → Computer Network Architect.
  - Enjoys math + statistics + machine learning → Data Scientist.

- Once enough information is collected, the bot:
  - Suggests **one or more** job types.
  - For each suggested role, provides:
    - A **one- or two-sentence summary** of what the role does.
    - The **skills** that are especially relevant.
    - Why the student’s answers align with that path.

### 4. Follow-Up Questions

After giving recommendations, the bot can:

- Offer to:
  - Explain **day-to-day tasks** for a role.
  - Compare **two roles**.
  - Suggest next steps (courses, projects, internships) that align with that career.

- Respond to generic questions like:
  - “What does a DevOps engineer actually do?”
  - “Is data science right for someone who doesn’t like statistics?”
  - “What if I like both security and cloud?”

### 5. Fallback and Help

- A **help** topic explains:
  - What the bot can do.
  - How to start over.
  - What kinds of questions it understands.
- A **catch-all** pattern (in `udc.aiml`) provides a sensible response when the bot does not recognize the input and tries to steer the conversation back to career guidance.

---

## How It Works (AIML Design)

This bot is built with AIML (Artificial Intelligence Markup Language) and runs on the Pandorabots platform.

Key design elements:

1. **Conversation Flow (`begin.aiml`, `help.aiml`)**
   - Handles greetings, introductions, and help messages.
   - Sets up the “session variables” Pandorabots uses to track user state.

2. **Role-Specific Files**
   Each career path has its own AIML file that:
   - Detects relevant signals from user input (e.g., “I like configuring servers”, “I enjoy statistics”).
   - Sets internal variables or adds “points” toward that job type.
   - Provides detailed descriptions when the user asks about that role by name.

   Files:
   - `devopsengineer.aiml`
   - `vulnerabilityresearch.aiml`
   - `cloudconsultant.aiml`
   - `computernetworkarchitect.aiml`
   - `datascientist.aiml`

3. **Fallback and “Universal” Patterns (`udc.aiml`)**
   - Captures more generic career questions.
   - Redirects the student back into a guided flow when possible.

4. **Substitution Files**
   - `normal.substitution`, `denormal.substitution`, `person.substitution`, `person2.substitution`, `gender.substitution`
   - Normalize user input (e.g., “I’m” → “I am”), handle pronouns, and improve pattern matching reliability.

5. **Bot Configuration (`.properties`)**
   - Stores bot metadata and configuration used by Pandorabots.
   - Defines the bot’s name and which AIML files are loaded.

