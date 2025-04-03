## Detailed Walkthrough: Stable Matching with 6 Students
### Example Setup
- **Students:** S1, S2, S3, S4, S5, S6
- **Hospitals:** H1, H2
- **Capacities:**
  - H1: 1 student
  - H2: 2 students
### Preference Lists
#### Student Preferences
(All students have an ordered list; here we choose lists so that many try H1 first.)
- S1: [H1, H2]
- S2: [H1, H2]
- S3: [H1, H2]
- S4: [H1, H2]
- S5: [H2, H1]   *(S5 prefers H2 first)*
- S6: [H2, H1]   *(S6 prefers H2 first)*
#### Hospital Preferences
- **H1:** [S2, S1, S3, S4, S5, S6]  
  (H1 ranks S2 highest, then S1, then S3, S4, …)
- **H2:** [S5, S6, S1, S2, S3, S4]  
  (H2 ranks S5 highest, then S6, then S1, …)
### Initial Data Structures
- **`assigned`:**
```python
  {"H1": [], "H2": []}
```
- **student_next_choice**:
```python
{"S1": 0, "S2": 0, "S3": 0, "S4": 0, "S5": 0, "S6": 0}
```
- **free_students**:
```python
{"S1", "S2", "S3", "S4", "S5", "S6"}
```
