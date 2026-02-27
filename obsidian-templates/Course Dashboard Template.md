---
type: course-dashboard
course: "{{COURSE_NAME}}"
code: "{{COURSE_CODE}}"
semester: "{{SEMESTER}}"
year: {{YEAR}}
professor: "{{PROFESSOR_NAME}}"
credits: {{CREDITS}}
tags: [{{COURSE_CODE}}, dashboard, {{SEMESTER}}]
---

# {{COURSE_CODE}}: {{COURSE_NAME}}

## 📊 Course Overview

| Field | Details |
|-------|---------|
| **Course Code** | {{COURSE_CODE}} |
| **Credits** | {{CREDITS}} |
| **Semester** | {{SEMESTER}} {{YEAR}} |
| **Professor** | {{PROFESSOR_NAME}} |
| **Email** | {{PROFESSOR_EMAIL}} |
| **Office Hours** | {{OFFICE_HOURS}} |
| **Class Schedule** | {{CLASS_SCHEDULE}} |
| **Location** | {{LOCATION}} |

---

## 🎯 Course Information

### Description
{{COURSE_DESCRIPTION}}

### Learning Objectives
1. Objective 1
2. Objective 2
3. Objective 3
4. Objective 4

### Prerequisites
- [[Course 1]]
- [[Course 2]]

---

## 📈 Grade Tracking

### Current Grade: {{CURRENT_GRADE}}% ({{LETTER_GRADE}})

### Grade Distribution

| Component | Weight | Earned | Possible | Percentage |
|-----------|--------|--------|----------|------------|
| Assignments | {{WEIGHT}}% | {{EARNED}} | {{POSSIBLE}} | {{PERCENT}}% |
| Quizzes | {{WEIGHT}}% | {{EARNED}} | {{POSSIBLE}} | {{PERCENT}}% |
| Midterm | {{WEIGHT}}% | {{EARNED}} | {{POSSIBLE}} | {{PERCENT}}% |
| Final Exam | {{WEIGHT}}% | {{EARNED}} | {{POSSIBLE}} | {{PERCENT}}% |
| Participation | {{WEIGHT}}% | {{EARNED}} | {{POSSIBLE}} | {{PERCENT}}% |
| **Total** | **100%** | **{{TOTAL_EARNED}}** | **{{TOTAL_POSSIBLE}}** | **{{CURRENT_GRADE}}%** |

### Grade Needed for Target

**Target Grade**: {{TARGET_GRADE}}%

**Points Still Available**: {{AVAILABLE_POINTS}}

**Points Needed**: {{POINTS_NEEDED}}

**Average Needed on Remaining Work**: {{AVERAGE_NEEDED}}%

---

## 📚 Lectures

### Recent Lectures
```dataview
TABLE date as "Date", topic as "Topic", status as "Status"
FROM "{{COURSE_NAME}}"
WHERE type = "lecture-notes"
SORT date DESC
LIMIT 10
```

### All Lectures
- [[Week 1 - {{TOPIC}}]]
- [[Week 2 - {{TOPIC}}]]
- [[Week 3 - {{TOPIC}}]]
- [[Week 4 - {{TOPIC}}]]

---

## ✅ Assignments

### Active Assignments
```dataview
TABLE due as "Due Date", status as "Status", grade as "Grade"
FROM "{{COURSE_NAME}}"
WHERE type = "assignment" AND status != "completed"
SORT due ASC
```

### Upcoming Deadlines
- [ ] {{ASSIGNMENT_NAME}} - Due: {{DUE_DATE}}
- [ ] {{ASSIGNMENT_NAME}} - Due: {{DUE_DATE}}
- [ ] {{ASSIGNMENT_NAME}} - Due: {{DUE_DATE}}

### Completed Assignments
```dataview
TABLE submitted as "Submitted", grade as "Grade", max-points as "Max Points"
FROM "{{COURSE_NAME}}"
WHERE type = "assignment" AND status = "completed"
SORT submitted DESC
```

### Assignment Statistics
- **Total Assignments**: {{TOTAL}}
- **Completed**: {{COMPLETED}}
- **Pending**: {{PENDING}}
- **Average Grade**: {{AVG_GRADE}}%
- **Highest Grade**: {{HIGHEST}}%
- **Lowest Grade**: {{LOWEST}}%

---

## 📝 Quizzes & Tests

### Upcoming Assessments
- [ ] Quiz {{NUMBER}} - {{DATE}} - Topics: {{TOPICS}}
- [ ] Midterm - {{DATE}} - Chapters {{CHAPTERS}}
- [ ] Final Exam - {{DATE}} - Comprehensive

### Past Assessments
| Assessment | Date | Grade | Topics Covered |
|------------|------|-------|----------------|
| Quiz 1 | {{DATE}} | {{GRADE}} | {{TOPICS}} |
| Quiz 2 | {{DATE}} | {{GRADE}} | {{TOPICS}} |
| Midterm | {{DATE}} | {{GRADE}} | {{TOPICS}} |

---

## 🔬 Lab Work / Projects

### Active Labs
```dataview
TABLE due as "Due Date", status as "Status"
FROM "{{COURSE_NAME}}"
WHERE type = "lab" AND status != "completed"
SORT due ASC
```

### Projects
- [[Project 1 - {{TITLE}}]] - Status: {{STATUS}}
- [[Project 2 - {{TITLE}}]] - Status: {{STATUS}}

---

## 📖 Study Materials

### Textbooks
- **Primary**: {{TEXTBOOK_NAME}} by {{AUTHOR}}
- **Secondary**: {{TEXTBOOK_NAME}} by {{AUTHOR}}

### Online Resources
- Course Website: [Link]({{URL}})
- Lecture Recordings: [Link]({{URL}})
- Practice Problems: [Link]({{URL}})

### Study Aids Created
- [[Summary Notes - {{TOPIC}}]]
- [[Flashcard Set - {{TOPIC}}]]
- [[Practice Problems - {{TOPIC}}]]

---

## 🗓️ Important Dates

| Date | Event |
|------|-------|
| {{DATE}} | First Day of Class |
| {{DATE}} | Midterm Exam |
| {{DATE}} | Project Due |
| {{DATE}} | Final Exam |
| {{DATE}} | Last Day of Class |

---

## 🎯 Weekly Focus

### This Week (Week {{WEEK_NUMBER}})
**Topics**: {{TOPICS}}

**To Do**:
- [ ] Attend lecture on {{DATE}}
- [ ] Complete reading: {{READING}}
- [ ] Work on {{ASSIGNMENT}}
- [ ] Review lecture notes
- [ ] Prepare for quiz

**Study Time Allocated**: {{HOURS}} hours

---

## 📊 Study Analytics

### Time Tracking
- **Total Study Hours**: {{TOTAL_HOURS}}
- **Average per Week**: {{AVG_HOURS}}
- **This Week**: {{THIS_WEEK_HOURS}}

### Performance Trends
📈 Improving / 📉 Declining / ➡️ Stable

**Strengths**: {{STRENGTHS}}

**Areas to Improve**: {{IMPROVEMENTS}}

---

## 💡 Key Concepts Map

### Major Topics
1. **{{TOPIC_1}}**
   - Subtopic A
   - Subtopic B
   - Related to: [[Other Course Topic]]

2. **{{TOPIC_2}}**
   - Subtopic A
   - Subtopic B
   - Related to: [[Other Course Topic]]

3. **{{TOPIC_3}}**
   - Subtopic A
   - Subtopic B
   - Related to: [[Other Course Topic]]

---

## 🤝 Study Resources

### Study Group
- Member 1: {{NAME}} - {{CONTACT}}
- Member 2: {{NAME}} - {{CONTACT}}
- Meeting Time: {{TIME}}
- Location: {{LOCATION}}

### Office Hours Visits
| Date | Topics Discussed | Follow-up Needed |
|------|------------------|------------------|
| {{DATE}} | {{TOPICS}} | {{FOLLOW_UP}} |

### Tutoring
- Tutor: {{NAME}}
- Schedule: {{SCHEDULE}}
- Location: {{LOCATION}}

---

## ⚠️ Exam Preparation

### Midterm Prep
- [ ] Review all lecture notes (Weeks 1-7)
- [ ] Complete practice problems
- [ ] Create summary sheets
- [ ] Review past quizzes
- [ ] Attend review session

### Final Exam Prep
- [ ] Comprehensive review of all materials
- [ ] Focus on {{HIGH_WEIGHT_TOPICS}}
- [ ] Complete final practice exam
- [ ] Review midterm and corrections
- [ ] Create master summary sheet

---

## 📝 Notes & Reflections

### What's Working

### Challenges

### Adjustments Needed

---

## 🔗 Quick Links

- **Course Materials**: [[{{COURSE_NAME}}-Materials]]
- **All Lectures**: [[{{COURSE_NAME}}-Lectures]]
- **All Assignments**: [[{{COURSE_NAME}}-Assignments]]
- **All Labs**: [[{{COURSE_NAME}}-Labs]]
- **Exam Prep**: [[{{COURSE_NAME}}-Exam-Prep]]
- **Flashcards**: [[{{COURSE_NAME}}-Flashcards]]

---

**Last Updated**: {{DATE}}
**Semester Dashboard**: [[{{SEMESTER}}-{{YEAR}}-Dashboard]]