> All prompts used in the project are uploaded in this folder and in this readme for better readability.

# Skill Gap Analysis Prompt
Analyze the **@candidate_CV** and **@job_description** 
Identify the key skills, qualifications, and experience required in the job description and compare them with the candidate's profile from the CV. Consider any coach input provided: **@Coach_Input**
Provide a comprehensive skill gap analysis that identifies: 
  1) Skills and qualifications the candidate already possesses that match the job requirements.
  2) Skills, qualifications, or experience that the candidate is missing or needs to strengthen.
  3) The relative importance of each gap identified (critical, important, or nice-to-have).
Format your response in clear sections with bullet points where appropriate.

---

# Training Recommendation Prompt
Based on the @skill_gap_analysis, @candidate_CV, @job_description, and @coach_input, recommend specific training resources, courses, certifications, or learning paths to help the candidate bridge the identified skill gaps. 
For each recommendation, include: 
  1) The specific skill gap it addresses.
  2) Why is this training appropriate for the candidate's background?
  3) Estimated time commitment required.
  4) Whether it's free or paid (with approximate cost if paid).
  5) Links or names of specific resources where possible (online courses, books, certifications, etc.). 
Prioritize recommendations based on the importance of the skill gaps they address.

---

# Training Schedule Prompt
Based on the @training_recommendations and @coach_input, create a realistic, week-by-week schedule for completing the recommended training. 
The schedule should: 
  1) Prioritize critical skill gaps first,
  2) Account for a reasonable time commitment per week (assume the person is working full-time unless indicated otherwise in the CV or coach input),
  3) Include milestones and checkpoints to track progress,
  4) Span an appropriate timeframe based on the volume and complexity of training needed (typically 1-6 months),
  5) Include specific actions and goals for each week.
  6) The schedule should be realistic, achievable, and considering the candidate's current skill level as indicated in their CV.
