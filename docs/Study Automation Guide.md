
---
# Study Materials Automation System

**Automated Workflow using n8n, Google Classroom, Claude AI, and Obsidian**

---

## Table of Contents

1. Executive Summary
2. Current Workflow Analysis
3. System Architecture
4. Step-by-Step Automation Guide
5. Required Tools and Services
6. Implementation Steps
7. Optimization Recommendations
8. Troubleshooting Guide
9. Future Enhancements

---

## 1. Executive Summary

This document outlines a comprehensive automation system designed to streamline the academic workflow for students. The system automatically processes study materials from Google Classroom, generates AI-enhanced learning resources using Claude AI, and organizes everything in Obsidian for efficient knowledge management and task tracking.

**Key Benefits:**
- Saves 10-15 hours per week on manual file management and note organization
- Ensures all study materials are automatically backed up locally
- Generates supplementary learning materials (summaries, questions, flashcards) instantly
- Maintains a centralized, interconnected knowledge base
- Tracks assignments, deadlines, and academic progress automatically
- Creates a searchable, portable study archive

---

## 2. Current Workflow Analysis

### 2.1 Current Manual Process

1. **Step 1**: Monitor Google Classroom for new study materials (lecture notes, tutorials, quizzes, tests, assignments, homework, lab work, projects)
2. **Step 2**: Manually download files from Google Classroom
3. **Step 3**: Save copies to local storage for offline access
4. **Step 4**: Upload lecture notes to Claude AI
5. **Step 5**: Generate review questions, summaries, and flashcards using Claude
6. **Step 6**: Copy generated content from Claude
7. **Step 7**: Create/update notes in Obsidian
8. **Step 8**: Organize files and create links between related concepts
9. **Step 9**: Update task tracking for assignments and deadlines
10. **Step 10**: Record scores and grades manually

### 2.2 Pain Points Identified

- Time-consuming: 1-2 hours daily spent on manual file management
- Risk of missing new materials or assignment updates
- Inconsistent organization leading to difficulty finding materials
- Repetitive copying and pasting between platforms
- No automatic backup system
- Manual tracking of deadlines prone to human error
- Difficult to see relationships between topics across subjects

---

## 3. System Architecture

### 3.1 Component Overview

The system consists of six primary components working together:

- **Google Classroom API**: Source of study materials and assignments — Trigger for automation workflows
- **n8n**: Workflow automation engine — Orchestrates all automated processes
- **Local File System**: Backup storage — Stores all materials offline
- **Claude AI API**: AI processing engine — Generates learning materials
- **Obsidian Vault**: Knowledge management system — Central repository for organized notes
- **Google Drive (Optional)**: Cloud backup — Additional backup layer

### 3.2 Data Flow

1. Google Classroom → New material posted
2. n8n Webhook → Detects new content via polling or webhook
3. n8n Download Node → Downloads files to local storage
4. n8n File Processing → Extracts text from PDFs, images, etc.
5. Claude AI API → Processes content to generate:
   - Comprehensive summaries
   - Review questions with answers
   - Flashcards for key concepts
   - Mind map suggestions
6. n8n Obsidian Integration → Creates/updates notes with:
   - Original material (as attachment)
   - AI-generated content
   - Metadata (date, subject, type)
   - Links to related notes
7. n8n Task Management → Updates task tracking:
   - Due dates
   - Assignment status
   - Grade tracking

---

## 4. Step-by-Step Automation Guide

### 4.1 Prerequisites

- Google Classroom account with active courses
- Claude AI API access (via Anthropic Console)
- n8n installed (self-hosted or cloud version)
- Obsidian installed with desired vault created
- Basic understanding of JSON and API concepts
- Local storage space (recommend 50GB+ available)

### 4.2 Setup Google Classroom API Access

**Step 1: Create a Google Cloud Project**
1. Go to https://console.cloud.google.com/
2. Create a new project (e.g., "Study Automation")
3. Note your Project ID

**Step 2: Enable Google Classroom API**
1. In your project, go to "APIs & Services" → "Library"
2. Search for "Google Classroom API"
3. Click "Enable"

**Step 3: Create OAuth 2.0 Credentials**
1. Go to "APIs & Services" → "Credentials"
2. Click "Create Credentials" → "OAuth client ID"
3. Choose "Desktop app" as application type
4. Download the JSON credentials file
5. Save securely (you'll need this for n8n)

**Step 4: Set OAuth Consent Screen**
1. Go to "OAuth consent screen"
2. Select "External" user type
3. Add your email as a test user
4. Add required scopes:
   - https://www.googleapis.com/auth/classroom.courses.readonly
   - https://www.googleapis.com/auth/classroom.coursework.me.readonly
   - https://www.googleapis.com/auth/classroom.announcements.readonly

### 4.3 Setup Claude AI API Access

**Step 1: Create Anthropic Account**
1. Go to https://console.anthropic.com/
2. Sign up for an account
3. Verify your email

**Step 2: Generate API Key**
1. Navigate to "API Keys" section
2. Click "Create Key"
3. Name it "n8n Study Automation"
4. Copy the key immediately (shown only once)
5. Store securely in a password manager

**Step 3: Set Up Billing (if required)**
1. Add payment method in console
2. Set usage limits to prevent unexpected charges
3. Recommended: Set budget alerts at $10, $25, $50

**Step 4: Test API Access**

Run this test command in terminal:
```bash
curl https://api.anthropic.com/v1/messages \
  -H "x-api-key: YOUR_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "content-type: application/json" \
  -d '{
    "model": "claude-sonnet-4-20250514",
    "max_tokens": 1024,
    "messages": [{"role": "user", "content": "Test"}]
  }'
```

### 4.4 Install and Configure n8n

**Option A: Self-Hosted with Docker (Recommended)**

1. Install Docker Desktop for your OS
2. Create a docker-compose.yml file:

```yaml
version: '3.8'
services:
  n8n:
    image: n8nio/n8n
    restart: always
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=changeme123
      - GENERIC_TIMEZONE=America/New_York
    volumes:
      - ~/.n8n:/home/node/.n8n
      - /path/to/study/materials:/data/study-materials
```

3. Run: `docker-compose up -d`
4. Access n8n at http://localhost:5678
5. Login with credentials from docker-compose.yml

**Option B: n8n Cloud**

1. Go to https://n8n.io/
2. Sign up for n8n Cloud (free tier available)
3. Create your instance
4. Note your instance URL

**Initial Configuration:**

1. Add Google Classroom credentials:
   - Settings → Credentials → Add Credential
   - Select "Google Classroom OAuth2 API"
   - Upload your JSON credentials file
   - Complete OAuth flow

2. Add Claude AI credentials:
   - Settings → Credentials → Add Credential
   - Select "HTTP Request" (Custom)
   - Add header: x-api-key: YOUR_CLAUDE_KEY

3. Configure file storage paths:
   - Settings → Variables
   - Add: LOCAL_STORAGE_PATH = /data/study-materials
   - Add: OBSIDIAN_VAULT_PATH = /path/to/obsidian/vault

---

## 5. Required Tools and Services

### 5.1 Core Tools

| Tool | Purpose | Cost | Setup Time |
|------|---------|------|------------|
| n8n | Workflow automation | Free (self-hosted) or $20/mo (cloud) | 1-2 hours |
| Google Classroom API | Access study materials | Free | 30 minutes |
| Claude AI API | Generate learning materials | Pay-per-use (~$5-15/mo estimated) | 15 minutes |
| Obsidian | Knowledge management | Free | 30 minutes |
| Docker (optional) | Host n8n locally | Free | 30 minutes |

### 5.2 Optional Enhancements

- Google Drive API: Additional cloud backup layer
- Telegram Bot: Get notifications of new assignments
- Dataview Plugin (Obsidian): Advanced query capabilities for task tracking
- Templater Plugin (Obsidian): Template automation
- Git: Version control for your Obsidian vault
- Anki: Integration for spaced repetition flashcards

---

## 6. Implementation Steps

### 6.1 Workflow 1: Google Classroom Monitor

**Purpose**: Automatically detect and download new materials from Google Classroom

**n8n Workflow Structure:**

**Node 1: Schedule Trigger (or Webhook)**
- Type: Schedule Trigger
- Settings: Run every 30 minutes
- Alternative: Use Google Classroom webhook if available

**Node 2: Get Classroom Courses**
- Type: HTTP Request
- Method: GET
- URL: https://classroom.googleapis.com/v1/courses
- Authentication: Use Google OAuth2 credentials
- Output: List of all your active courses

**Node 3: Loop Through Courses**
- Type: Loop Over Items (SplitInBatches)
- Batch size: 1
- Keep: Process each course individually

**Node 4: Get Course Materials**
- Type: HTTP Request
- Method: GET
- URL: https://classroom.googleapis.com/v1/courses/{{$node["Get Classroom Courses"].json["id"]}}/courseWork
- Filter: Only new items (compare with last check timestamp)

**Node 5: Check for New Materials**
- Type: IF
- Condition: {{ $json.updateTime > $node["Get Last Check"].json["lastCheckTime"] }}
- True path: Continue processing
- False path: Skip (already processed)

**Node 6: Download Material Files**
- Type: HTTP Request
- Method: GET
- URL: {{ $json.materials[0].driveFile.driveFile.alternateLink }}
- Save as binary file

**Node 7: Save to Local Storage**
- Type: Write Binary File
- File path: {{$env.LOCAL_STORAGE_PATH}}/{{$json.courseName}}/{{$json.title}}.{{$json.fileExtension}}
- Create directories if needed

**Node 8: Update Last Check Timestamp**
- Type: Set
- Update JSON with current timestamp
- Store in n8n database or file

### 6.2 Workflow 2: AI Content Generation

**Purpose**: Process downloaded materials through Claude AI to generate learning resources

**n8n Workflow Structure:**

**Node 1: File Watcher (or follows Workflow 1)**
- Type: File trigger or direct connection from Workflow 1
- Watch: {{$env.LOCAL_STORAGE_PATH}}/**/*
- Filter: Only process .pdf, .docx, .pptx, .txt files

**Node 2: Extract Text Content**
- Type: Code node (JavaScript)
- For PDFs: Use pdf-parse library
- For DOCX: Use mammoth library
- For PPTX: Use pptx-parser
- Output: Plain text content

**Node 3: Classify Content Type**
- Type: Switch
- Based on: File name or content analysis
- Routes:
  - Lecture Notes → Generate summaries + questions + flashcards
  - Tutorial → Generate practice problems + solutions
  - Assignment → Extract requirements + create checklist

**Node 4: Call Claude AI API**
- Type: HTTP Request
- Method: POST
- URL: https://api.anthropic.com/v1/messages
- Headers:
  - x-api-key: {{$env.CLAUDE_API_KEY}}
  - anthropic-version: 2023-06-01
  - content-type: application/json
- Body (for lecture notes):

```json
{
  "model": "claude-sonnet-4-20250514",
  "max_tokens": 4096,
  "messages": [{
    "role": "user",
    "content": "Based on this lecture content, please create:\n\n1. A comprehensive summary (300-500 words)\n2. 10 review questions with detailed answers\n3. 15 flashcards in the format 'Q: [question] | A: [answer]'\n4. Key concepts and their relationships\n\nLecture Content:\n{{$node["Extract Text Content"].json["text"]}}"
  }]
}
```

**Node 5: Parse Claude Response**
- Type: Code node
- Parse JSON response
- Structure output into sections:
  - summary
  - questions
  - flashcards
  - concepts

**Node 6: Format for Obsidian**
- Type: Code node
- Generate markdown content with frontmatter:

```markdown
---
type: lecture-notes
subject: {{$json.courseName}}
date: {{$json.date}}
source: {{$json.filename}}
tags: [{{$json.courseName}}, lecture, ai-generated]
---

# {{$json.title}}

## Summary
{{$json.summary}}

## Review Questions
{{$json.questions}}

## Flashcards
{{$json.flashcards}}

## Key Concepts
{{$json.concepts}}

## Original Material
![[{{$json.filename}}]]
```

### 6.3 Workflow 3: Obsidian Integration

**Purpose**: Create and organize notes in Obsidian vault with proper linking

**n8n Workflow Structure:**

**Node 1: Receives from Workflow 2**
- Input: Formatted markdown content

**Node 2: Create Note File**
- Type: Write Binary File
- Path: {{$env.OBSIDIAN_VAULT_PATH}}/{{$json.courseName}}/{{$json.title}}.md
- Content: {{$json.markdownContent}}

**Node 3: Attach Original File**
- Type: Write Binary File
- Path: {{$env.OBSIDIAN_VAULT_PATH}}/attachments/{{$json.filename}}
- Content: Original file binary

**Node 4: Update Course Index**
- Type: Read/Write File
- Read: {{$env.OBSIDIAN_VAULT_PATH}}/{{$json.courseName}}/README.md
- Append: Link to new note with date
- Example: - [[{{$json.title}}]] - {{$json.date}}

**Node 5: Create Concept Links**
- Type: Code node
- Extract mentioned concepts from content
- Search existing notes for related concepts
- Generate links: [[Concept Name]]

**Node 6: Update Graph Relationships**
- Type: Code node
- Create MOC (Map of Content) note if needed
- Link related topics across courses
- Example: Link "Linear Algebra" concepts to "Machine Learning" notes

**Node 7: Update Task Tracking (if assignment)**
- Type: IF → Check if assignment
- True path:
  - Create task in designated task note
  - Format: - [ ] {{$json.title}} | Due: {{$json.dueDate}} | Course: {{$json.courseName}}
  - Add to course task list

### 6.4 Workflow 4: Task and Grade Tracking

**Purpose**: Maintain assignment tracking and grade recording

**n8n Workflow Structure:**

**Node 1: Assignment Detector**
- Type: IF node from Workflow 1
- Condition: courseWork.workType === "ASSIGNMENT"
- Extract: title, dueDate, maxPoints, description

**Node 2: Create Task Entry**
- Type: Code node
- Generate task markdown:

```markdown
- [ ] {{title}}
  - Course: [[{{courseName}}]]
  - Due: {{dueDate}}
  - Points: {{maxPoints}}
  - Status: Not Started
  - Link: [[{{noteTitle}}]]
```

**Node 3: Add to Master Task List**
- Type: Write File
- Path: {{$env.OBSIDIAN_VAULT_PATH}}/Tasks/Active-Assignments.md
- Mode: Append

**Node 4: Add to Course Task List**
- Type: Write File
- Path: {{$env.OBSIDIAN_VAULT_PATH}}/{{courseName}}/Tasks.md
- Mode: Append

**Node 5: Set Deadline Reminder**
- Type: Schedule Trigger
- Create trigger for 2 days before due date
- Create trigger for 1 day before due date

**Node 6: Monitor Grade Updates**
- Type: HTTP Request (periodic)
- URL: https://classroom.googleapis.com/v1/courses/{{courseId}}/courseWork/{{workId}}/studentSubmissions
- Check for grade updates

**Node 7: Update Grade Records**
- Type: Code + Write File
- When grade received:
  - Update task status to "Completed"
  - Record grade: {{grade}}/{{maxPoints}}
  - Calculate percentage
  - Update grade tracker

**Node 8: Update Statistics**
- Type: Code node
- Update course statistics note:
  - Average grade
  - Completion rate
  - Pending assignments count
  - Grade distribution chart data

---

## 7. Optimization Recommendations

### 7.1 Immediate Improvements

**Batch Processing**: Process multiple files in single Claude API call to reduce API costs and time. Group materials by course or topic.

**Smart Caching**: Store checksums of processed files to avoid reprocessing unchanged materials. Saves API calls and processing time.

**Error Handling**: Add comprehensive error handling with retry logic. Failed downloads or API calls should retry 3 times with exponential backoff.

**Notification System**: Integrate Telegram or Discord bot for instant notifications when new assignments are posted or deadlines are approaching.

**Template System**: Create Obsidian templates for different material types (lectures, assignments, labs) for consistent formatting.

**Backup Strategy**: Implement automated backups to Google Drive or Dropbox daily. Keep 7-day version history.

### 7.2 Advanced Enhancements

**Spaced Repetition Integration**: Export flashcards to Anki automatically with scheduling algorithm. Use AnkiConnect API for seamless integration.

**Citation Management**: Extract references from materials and build bibliography automatically using Zotero integration.

**Study Session Analytics**: Track time spent on each subject using Obsidian plugins. Generate weekly study reports with visualizations.

**Collaborative Features**: Share notes with study group via Obsidian Sync or Git. Track contributions and maintain version control.

**Voice Note Processing**: Record lectures and use Whisper API to transcribe. Process transcriptions through Claude for note generation.

**Smart Scheduling**: Use AI to analyze your calendar and suggest optimal study times based on assignment complexity and deadlines.

**Performance Prediction**: Analyze grade trends and study patterns to predict performance and suggest focus areas for improvement.

### 7.3 Cost Optimization

**Claude API Cost Management:**

1. **Use Claude Haiku for simple tasks:**
   - Haiku: $0.25 per MTok (input), $1.25 per MTok (output)
   - Sonnet: $3 per MTok (input), $15 per MTok (output)
   - Use Haiku for flashcard generation, simple summaries
   - Use Sonnet for complex analysis, detailed explanations

2. **Implement content filtering:**
   - Only process materials that actually need AI enhancement
   - Skip processing for simple handouts, schedules, syllabi
   - Use file size and type filters

3. **Optimize prompts:**
   - Keep prompts concise but specific
   - Use system prompts to reduce repeated instructions
   - Request structured output (JSON) to minimize parsing errors

4. **Estimated Monthly Costs:**
   - Light usage (10 documents/week): $5-10/month
   - Moderate usage (25 documents/week): $15-25/month
   - Heavy usage (50+ documents/week): $30-50/month

5. **Free alternatives for specific tasks:**
   - Use local OCR (Tesseract) instead of Claude for text extraction
   - Use Obsidian plugins for flashcard generation from notes
   - Generate summaries only for complex lectures, not all materials

---

## 8. Troubleshooting Guide

### Google Classroom API not returning data

- Verify OAuth2 credentials are valid and not expired
- Check API is enabled in Google Cloud Console
- Ensure scopes include classroom.courses.readonly
- Test API access with curl command

### Claude API rate limit errors

- Implement exponential backoff retry logic
- Reduce batch sizes for concurrent requests
- Monitor usage in Anthropic Console
- Consider upgrading API tier if consistent limits

### Files not downloading correctly

- Check LOCAL_STORAGE_PATH variable is correct
- Verify directory permissions (mkdir -p to create)
- Ensure sufficient disk space available
- Check file type filters in workflow

### Obsidian notes not appearing

- Verify OBSIDIAN_VAULT_PATH points to correct vault
- Check Obsidian is not running when files are written
- Verify markdown syntax is valid
- Look for special characters in filenames (sanitize)

### n8n workflows failing silently

- Enable debug mode in n8n settings
- Check execution logs for error messages
- Verify all credentials are properly configured
- Test nodes individually before combining

---

## 9. Future Enhancements

**Phase 1 (Months 1-2):**
- Implement basic automation workflows
- Establish consistent naming conventions
- Set up backup systems
- Fine-tune Claude prompts for your specific courses

**Phase 2 (Months 3-4):**
- Add notification systems (Telegram/Discord)
- Implement spaced repetition with Anki
- Create custom Obsidian templates
- Build analytics dashboard for study patterns

**Phase 3 (Months 5-6):**
- Integrate citation management
- Add voice note processing
- Implement collaborative features
- Create mobile workflow optimizations

**Phase 4 (Long-term):**
- Machine learning for personalized study recommendations
- Predictive analytics for exam preparation
- Integration with LMS platforms beyond Google Classroom
- Community sharing of workflows and templates
- Cross-platform synchronization (iOS, Android, Web)

**Potential Integrations:**
- Notion API for alternative knowledge base
- Trello/Asana for advanced project management
- Zapier for additional automation triggers
- GitHub for version control of study materials
- Mendeley/Zotero for research paper management
- Wolfram Alpha API for STEM problem solving
- Grammarly API for writing improvement
- Forest App API for productivity tracking

---

## Appendix A: n8n Workflow JSON Templates

Complete workflow JSON templates will be provided in separate files:
- 1-google-classroom-monitor.json
- 2-ai-content-generation.json
- 3-obsidian-integration.json
- 4-task-grade-tracking.json

## Appendix B: Useful Resources

- n8n Documentation: https://docs.n8n.io/
- Google Classroom API: https://developers.google.com/classroom
- Claude AI Documentation: https://docs.anthropic.com/
- Obsidian Documentation: https://help.obsidian.md/
- Markdown Guide: https://www.markdownguide.org/
- Regular Expressions Guide: https://regexr.com/

## Appendix C: Cost Breakdown

**Detailed Monthly Cost Estimates:**

**Self-Hosted Setup:**
- n8n: $0 (self-hosted with Docker)
- Server/VPS (optional): $5-10/month
- Claude API: $10-30/month (usage-based)
- Total: $15-40/month

**Cloud Setup:**
- n8n Cloud: $20/month
- Claude API: $10-30/month
- Total: $30-50/month

**One-time Costs:**
- Domain name (optional): $10-15/year
- None for local setup

**Time Investment:**
- Initial setup: 8-12 hours
- Weekly maintenance: 1-2 hours
- ROI: Saves 10-15 hours/week on manual tasks

The automation pays for itself by freeing up time for actual studying and improving grade outcomes through better organization and review materials.

---

---