---
type: weekly-review
week: "Week {{WEEK_NUMBER}}"
start-date: {{START_DATE}}
end-date: {{END_DATE}}
semester: "{{SEMESTER}} {{YEAR}}"
tags: [weekly-review, productivity, {{SEMESTER}}]
---

# Week {{WEEK_NUMBER}} Review - {{START_DATE}} to {{END_DATE}}

## 📊 Week at a Glance

| Metric | Value |
|--------|-------|
| **Study Hours** | {{STUDY_HOURS}} hours |
| **Assignments Completed** | {{COMPLETED}}/{{TOTAL}} |
| **New Materials Processed** | {{MATERIALS_COUNT}} |
| **Notes Created** | {{NOTES_COUNT}} |
| **Average Grade** | {{AVG_GRADE}}% |
| **Lectures Attended** | {{ATTENDED}}/{{SCHEDULED}} |

---

## ✅ Accomplishments

### Academic Wins
- 
- 
- 

### Learning Highlights
- 
- 
- 

### Automation Performance
- Files auto-downloaded: {{AUTO_DOWNLOADS}}
- AI-generated content pieces: {{AI_CONTENT}}
- Time saved by automation: ~{{TIME_SAVED}} hours

---

## 📚 By Course

### {{CS311}}
- **Topics Covered**: 
- **Assignments**: 
- **Grade Status**: 
- **Notes to Self**: 

### {{CS312}}
- **Topics Covered**: 
- **Assignments**: 
- **Grade Status**: 
- **Notes to Self**: 

### {{CS313}}
- **Topics Covered**: 
- **Assignments**: 
- **Grade Status**: 
- **Notes to Self**: 

### {{CS314}}
- **Topics Covered**: 
- **Assignments**: 
- **Grade Status**: 
- **Notes to Self**: 

---

## 📋 Tasks Completed This Week

```dataview
TABLE status as "Status", course as "Course"
FROM "Tasks"
WHERE completed >= date("{{START_DATE}}") AND completed <= date("{{END_DATE}}")
```

**Manual List**:
- [x] Task 1
- [x] Task 2
- [x] Task 3

---

## ⏰ Upcoming This Week

### Deadlines (Next 7 Days)
- [ ] {{ASSIGNMENT}} - {{COURSE}} - Due: {{DATE}}
- [ ] {{ASSIGNMENT}} - {{COURSE}} - Due: {{DATE}}
- [ ] {{ASSIGNMENT}} - {{COURSE}} - Due: {{DATE}}

### Exams/Quizzes
- [ ] {{ASSESSMENT}} - {{COURSE}} - Date: {{DATE}}

### Other Commitments
- [ ] 
- [ ] 

---

## 💡 Insights & Reflections

### What Worked Well

### What Didn't Work

### Lessons Learned

### Concepts Mastered This Week
1. 
2. 
3. 

### Areas Needing More Focus
1. 
2. 
3. 

---

## 📈 Progress Tracking

### Goals from Last Week
- [ ] Goal 1 - Status:
- [ ] Goal 2 - Status:
- [ ] Goal 3 - Status:

### Goals for Next Week
1. 
2. 
3. 

### Long-term Progress
- Overall GPA: {{GPA}}
- Target GPA: {{TARGET_GPA}}
- Gap: {{GAP}}

---

## ⚙️ Automation Performance

### System Health
- ✅ All workflows running smoothly
- ⚠️ Minor issues (describe):
- ❌ Major issues (describe):

### Claude API Usage
- Requests this week: {{REQUESTS}}
- Estimated cost: ${{COST}}
- Content quality rating: {{RATING}}/10

### Improvements Made
- 
- 

### Adjustments Needed
- 
- 

---

## 🎯 Study Effectiveness

### Time Allocation

| Activity | Hours | % of Total |
|----------|-------|------------|
| Lectures | {{HOURS}} | {{PERCENT}}% |
| Reading | {{HOURS}} | {{PERCENT}}% |
| Assignments | {{HOURS}} | {{PERCENT}}% |
| Review/Study | {{HOURS}} | {{PERCENT}}% |
| Projects | {{HOURS}} | {{PERCENT}}% |

### Productivity Score
**Overall**: {{SCORE}}/10

**Breakdown**:
- Focus quality: {{SCORE}}/10
- Time management: {{SCORE}}/10
- Task completion: {{SCORE}}/10
- Material retention: {{SCORE}}/10

---

## 🔗 Key Connections Made

### New Links Created Between Concepts
- [[Concept A]] ↔ [[Concept B]] - Relationship:
- [[Topic X]] ↔ [[Topic Y]] - Relationship:

### Cross-Course Insights
- 

---

## 📝 Action Items for Next Week

### High Priority
- [ ] 
- [ ] 
- [ ] 

### Medium Priority
- [ ] 
- [ ] 

### Low Priority
- [ ] 
- [ ] 

### Automation Tweaks
- [ ] 
- [ ] 

---

## 🎊 Celebrate

### Small Wins
- 
- 
- 

### Something I'm Proud Of

---

## 📸 Weekly Snapshot

**Overall Rating**: {{RATING}}/10

**One Word to Describe This Week**: {{WORD}}

**Most Valuable Learning**: 

**Quote of the Week**: 

---

**Previous Week**: [[Week {{PREV_WEEK}} Review]]
**Next Week**: [[Week {{NEXT_WEEK}} Review]]
**Monthly Review**: [[{{MONTH}} {{YEAR}} Review]]