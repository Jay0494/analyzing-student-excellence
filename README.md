# INTRODUCTION
The Student Educational Excellence project is designed to analyze and improve student performance across key academic subjects—math, reading, and writing. Using a comprehensive dataset that includes scores, demographic factors, parental education levels, and participation in various school programs, the goal is to gain insights into the educational outcomes of students and identify areas for improvement. By leveraging data-driven strategies, this project seeks to enhance overall academic performance and address specific challenges faced by students across different demographic groups.
### **Data Processing Procedures**

The **Student Educational Excellence** project involved several data processing steps to ensure the dataset was clean, standardized, and ready for analysis. The following procedures were employed to transform the raw data into a format suitable for extracting insights:

#### **1. Data Cleaning in Power Query**
   - **Removing Empty Rows**: In Power Query, all empty or irrelevant rows were identified and removed to ensure that the dataset only contained valid entries. This helped to prevent inaccuracies in calculations and visualizations.
   - **Handling Missing Data**: Any missing or incomplete data points were addressed by either removing incomplete records or applying appropriate imputation methods where necessary.
   - **Filtering and Sorting Data**: Data was sorted by relevant columns such as gender, race/ethnicity, parental education, and subject scores to facilitate easier processing and analysis.

#### **2. Data Standardization**
   - **Standardizing Text Fields**: Categorical columns such as "gender," "race_ethnicity," "parental_level_of_education," and "test_preparation_course" were standardized. This involved ensuring consistency in text values (e.g., correcting variations like "Bachelor's Degree" and "bachelor's degree").
   - **Normalizing Scores**: Student scores in math, reading, and writing were checked for consistency. The data was formatted to ensure all scores were numeric, and appropriate decimal precision was applied.
   
#### **3. Calculated Columns in DAX**
   - **Maths Performance Category**: A new calculated column was introduced to categorize students into performance levels (Basic, Proficient, Advanced, Below Basic) based on their different scores. This allowed for more granular analysis of performance:
   ```SQL
   Maths performance = SWITCH(
                      TRUE(),
                        'School data'[math_score] <  50, "Below Basic",
                        'School data'[math_score] >= 50 && 'School data'[math_score] <= 69, "Basic",
                        'School data'[math_score] >= 70 && 'School data'[math_score] <= 89, "Proficient",
                        'School data'[math_score] >= 90, "Advanced",
                        "Not applicable"
)
   ```
   - **Performance Category**: A new calculated column was introduced to categorize students into performance levels (Basic, Proficient, Advanced, Below Basic) based on their writing scores. This allowed for more granular analysis of performance:
```SQL
Writing performance = SWITCH(
                        TRUE(),
                           'School data'[writing_score] < 50, "Below basic",
                           'School data'[writing_score] >= 50 && 'School data'[writing_score] <= 69, "Basic",
                           'School data'[writing_score] >= 70 && 'School data'[writing_score] <= 89, "Proficient",
                           'School data'[writing_score] >= 90, "Advanced",
                           "Not applicable"
)
```
  - **Performance Category**: A new calculated column was introduced to categorize students into performance levels (Basic, Proficient, Advanced, Below Basic) based on their READING scores. This allowed for more granular analysis of performance:
```SQL
Reading performance = SWITCH(
                        TRUE(),
                           'School data'[reading_score] < 50, "Below basic",
                           'School data'[reading_score] >= 50 && 'School data'[reading_score] <= 69, "Basic",
                           'School data'[reading_score] >= 70 && 'School data'[reading_score] <= 89, "Proficient",
                           'School data'[reading_score] >= 90, "Advanced",
                           "Not applicable"
)
```

Overall Average Score: A calculated measure was created in DAX to compute each student’s overall average score, based on the average of their math, reading, and writing scores. The formula used:
```SQL
Overall average = AVERAGEX('School data', 
                           'School data'[writing_score] + 'School data'[reading_score] + 'School data'[math_score])/3
```
#### **4. Data Transformation in Power BI**
   - **Data Modeling**: Relationships between different tables were established in Power BI’s data model, enabling seamless analysis across multiple dimensions
  
### **Tools Used**
   - **Power Query**: Used for initial data cleaning, transformation, and standardization.
   - **DAX (Data Analysis Expressions)**: Used to create calculated columns and measures, such as the overall average score and performance categories.
   - **Power BI**: Utilized for building the final dashboards, visualizations, and extracting insights through interactive data exploration.

These data processing steps ensured the dataset was properly cleaned, structured, and optimized for analysis, allowing for accurate identification of trends and insights into student performance.

### **Insights**

#### **Math Performance:**
- **Basic**: 45.6%
- **Proficient**: 35.1%
- **Below Basic**: 13.5%
- **Advanced**: 5.8%

#### **Reading Performance:**
- **Proficient**: 43.4%
- **Basic**: 39.7%
- **Below Basic**: 9.0%
- **Advanced**: 7.9%

#### **Writing Performance:**
- **Proficient**: 41.1%
- **Basic**: 39.7%
- **Below Basic**: 11.4%
- **Advanced**: 7.8%

#### **Total Students by Gender**:
- **Female**: 51.8%
- **Male**: 48.2%

#### **Overall Average Score by Gender**:
- **Female**: 51.38%
- **Male**: 48.6%

#### **Overall Average Score**:
- **Average Score**: 67.77

### **Recommendations:**

1. **Focus on Math Proficiency**:
   - With 45.6% of students in the "Basic" category and only 5.8% in "Advanced", there is a need to boost math proficiency. Additional targeted math interventions, such as tutoring or adaptive learning platforms, should be considered for students in the "Basic" and "Below Basic" categories.

2. **Improve Reading Performance**:
   - While 43.4% of students are proficient, only 7.9% are in the advanced category. Expanding programs that promote reading comprehension and critical thinking, like book clubs or enhanced reading assignments, could raise the number of advanced readers.

3. **Enhance Writing Skills**:
   - Writing performance shows a similar trend to reading, with only 7.8% of students in the advanced category. To encourage growth in writing skills, incorporate more writing-intensive assignments and feedback sessions. Consider introducing creative writing or essay contests to inspire students.

4. **Gender-Based Interventions**:
   - With a relatively balanced gender distribution (51.8% female, 48.2% male) but slightly higher average scores for females, consider exploring gender-specific teaching techniques. Analyze whether teaching strategies are equally effective for both genders, and ensure that any disparity in performance is addressed.

5. **Addressing the Needs of "Below Basic" Students**:
   - A significant portion of students (especially in math) are categorized as "Below Basic". These students need targeted support through remedial programs, individualized attention, or specialized resources that cater to foundational skills.


Despite the efforts made by educators and institutions to foster student learning, a significant percentage of students continue to underperform, particularly in mathematics and literacy skills. The analysis shows that a large portion of students fall into the "Basic" and "Below Basic" performance categories, with only a small percentage achieving "Advanced" levels. This trend is consistent across math, reading, and writing, which raises concerns about the overall effectiveness of current educational strategies and support systems.
### **Next Steps:**

1. **Conduct a Gap Analysis**:
   - Perform a deeper dive into why some students remain in the "Below Basic" or "Basic" categories. Investigate factors such as socio-economic background, learning disabilities, or access to resources that may be influencing their performance.

2. **Implement a Data-Driven Tutoring Program**:
   - Launch a tutoring or mentoring program that uses the performance data to prioritize students who are in the "Below Basic" and "Basic" categories. Focus on personalized learning plans to address specific skill gaps in math, reading, and writing.

3. **Professional Development for Teachers**:
   - Provide professional development focused on differentiated instruction to help teachers better meet the diverse learning needs of students, especially those who struggle. Include training on how to encourage higher-level thinking for students in the proficient range to push them toward advanced categories.

4. **Continuous Monitoring and Feedback**:
   - Develop dashboards or ongoing assessments to regularly track student progress, ensuring that interventions are effective. Set quarterly goals for moving students from "Basic" to "Proficient" or "Advanced".

5. **Engage Parents and Guardians**:
   - Involve parents in the process by sharing individual performance reports and offering resources they can use at home to support their children's learning. Regular parent-teacher meetings could discuss student progress and areas for improvement.

