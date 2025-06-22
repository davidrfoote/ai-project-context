# Claude Prompt Templates & Ready-to-Use Patterns

## Quick Start Templates

### 1. Universal Analysis Template
```xml
<analysis>
  <subject>[What you're analyzing]</subject>
  
  <data>
    [Insert your data/content here]
  </data>
  
  <requirements>
    <depth>[surface|moderate|deep]</depth>
    <perspective>[technical|business|user|balanced]</perspective>
    <output_format>[summary|detailed|executive]</output_format>
  </requirements>
  
  <focus_areas>
    - [Specific aspect 1]
    - [Specific aspect 2]
    - [Specific aspect 3]
  </focus_areas>
</analysis>

Please provide:
<results>
  <key_findings>3-5 main discoveries</key_findings>
  <detailed_analysis>In-depth examination</detailed_analysis>
  <recommendations>Actionable next steps</recommendations>
  <confidence_level>Your certainty about conclusions</confidence_level>
</results>
```

### 2. Code Review Master Template
```python
"""
Review this code for quality, performance, and best practices:

<code language="[python|javascript|java|etc]">
[INSERT YOUR CODE HERE]
</code>

<review_criteria>
  - Performance optimization opportunities
  - Security vulnerabilities
  - Code maintainability
  - Error handling completeness
  - Best practices adherence
  - Documentation quality
</review_criteria>

<context>
  - Purpose: [What this code does]
  - Constraints: [Any limitations]
  - Team standards: [Specific guidelines]
</context>

Provide feedback in this format:
<review>
  <summary>Overall assessment</summary>
  
  <issues>
    <critical>
      - Issue: [Description]
        Impact: [High/Medium/Low]
        Fix: [Specific solution]
        Example: [Code snippet]
    </critical>
    
    <improvements>
      [Suggestions for enhancement]
    </improvements>
  </issues>
  
  <positive>
    [What's done well]
  </positive>
  
  <refactored_version>
    [If major changes needed, provide refactored code]
  </refactored_version>
</review>
"""
```

### 3. Writing Enhancement Template
```xml
<writing_task>
  <original_text>
    [INSERT YOUR TEXT HERE]
  </original_text>
  
  <goals>
    <audience>[Target readers]</audience>
    <tone>[formal|casual|academic|persuasive]</tone>
    <purpose>[inform|persuade|entertain|instruct]</purpose>
    <length>[keep same|expand to X words|reduce by Y%]</length>
  </goals>
  
  <enhancement_focus>
    - Clarity and conciseness
    - Engagement and flow
    - Grammar and style
    - SEO optimization (if applicable)
    - Call-to-action strength
  </enhancement_focus>
</writing_task>

Please provide:
1. Enhanced version with track changes explanation
2. Summary of major improvements
3. Alternative approaches for key sections
4. SEO keywords naturally integrated (if applicable)
```

### 4. Decision-Making Framework
```xml
<decision_framework>
  <situation>
    [Describe the decision to be made]
  </situation>
  
  <options>
    <option id="A">
      <description>[Option A details]</description>
      <cost>[Financial/resource cost]</cost>
      <timeline>[Implementation time]</timeline>
    </option>
    <option id="B">
      <description>[Option B details]</description>
      <cost>[Financial/resource cost]</cost>
      <timeline>[Implementation time]</timeline>
    </option>
    <!-- Add more options as needed -->
  </options>
  
  <criteria>
    <criterion weight="high|medium|low">Cost efficiency</criterion>
    <criterion weight="high|medium|low">Time to market</criterion>
    <criterion weight="high|medium|low">Risk level</criterion>
    <criterion weight="high|medium|low">Strategic alignment</criterion>
    <!-- Add custom criteria -->
  </criteria>
  
  <constraints>
    - [Budget limits]
    - [Time constraints]
    - [Resource availability]
  </constraints>
</decision_framework>

Analyze using:
1. Weighted scoring matrix
2. Risk-benefit analysis
3. Best/worst case scenarios
4. Recommendation with confidence level
```

### 5. Learning Content Generator
```python
learning_template = """
Create educational content for: {topic}

<parameters>
  <audience>
    <level>[beginner|intermediate|advanced]</level>
    <background>[Expected prior knowledge]</background>
    <learning_style>[visual|auditory|kinesthetic|mixed]</learning_style>
  </audience>
  
  <format>
    <type>[lesson|tutorial|guide|reference]</type>
    <duration>[Estimated time to complete]</duration>
    <interactive>[yes|no]</interactive>
  </format>
</parameters>

<requirements>
  1. Learning objectives (3-5 specific, measurable goals)
  2. Pre-requisites clearly stated
  3. Step-by-step progression
  4. Examples for each concept
  5. Practice exercises with solutions
  6. Common misconceptions addressed
  7. Additional resources for deep dive
</requirements>

Structure the content as:
<lesson>
  <introduction>
    - Hook/attention grabber
    - Why this matters
    - What you'll learn
  </introduction>
  
  <main_content>
    <concept_1>
      <explanation>[Clear explanation]</explanation>
      <example>[Practical example]</example>
      <practice>[Exercise]</practice>
    </concept_1>
    <!-- Repeat for each concept -->
  </main_content>
  
  <summary>
    - Key takeaways
    - Quick reference
  </summary>
  
  <assessment>
    - Self-check questions
    - Project ideas
    - Next steps
  </assessment>
</lesson>
"""
```

### 6. API Documentation Template
```xml
<api_documentation>
  <endpoint>
    <name>[Endpoint name]</name>
    <method>[GET|POST|PUT|DELETE]</method>
    <path>[/api/v1/resource]</path>
  </endpoint>
  
  <functionality>
    [What this endpoint does]
  </functionality>
  
  <authentication>
    [Required auth method]
  </authentication>
  
  <generate_docs>
    1. Overview and purpose
    2. Request parameters (required/optional)
    3. Request body schema (if applicable)
    4. Response formats (success/error)
    5. Status codes and meanings
    6. Example requests (cURL, Python, JavaScript)
    7. Example responses
    8. Common errors and solutions
    9. Rate limits
    10. Best practices
  </generate_docs>
</api_documentation>
```

### 7. Bug Report Analysis
```python
bug_analysis = """
<bug_report>
  <description>
    [User's bug description]
  </description>
  
  <environment>
    <os>[Operating system]</os>
    <version>[Software version]</version>
    <browser>[If applicable]</browser>
    <hardware>[Relevant specs]</hardware>
  </environment>
  
  <steps_to_reproduce>
    1. [Step 1]
    2. [Step 2]
    3. [Step 3]
  </steps_to_reproduce>
  
  <expected>[What should happen]</expected>
  <actual>[What actually happens]</actual>
  
  <frequency>[always|sometimes|once]</frequency>
  
  <attachments>
    - Error logs
    - Screenshots
    - Stack traces
  </attachments>
</bug_report>

Analyze and provide:
<analysis>
  <severity>[Critical|High|Medium|Low]</severity>
  <category>[UI|Backend|Database|Network|Logic]</category>
  <root_cause>
    Most likely causes with confidence levels
  </root_cause>
  <impact>
    - Affected users
    - Business impact
    - Technical implications
  </impact>
  <investigation_steps>
    Ordered list of diagnostic steps
  </investigation_steps>
  <potential_fixes>
    - Quick workaround
    - Proper solution
    - Preventive measures
  </potential_fixes>
  <similar_issues>
    Related bugs or patterns
  </similar_issues>
</analysis>
"""
```

### 8. Strategy Development Template
```xml
<strategy_development>
  <context>
    <organization>[Company/team description]</organization>
    <current_situation>[Where you are now]</current_situation>
    <desired_outcome>[Where you want to be]</desired_outcome>
    <timeframe>[Timeline for change]</timeframe>
  </context>
  
  <market_analysis>
    <competitors>[Key competitors]</competitors>
    <trends>[Industry trends]</trends>
    <opportunities>[Market opportunities]</opportunities>
    <threats>[Potential threats]</threats>
  </market_analysis>
  
  <resources>
    <budget>[Available budget]</budget>
    <team>[Team capabilities]</team>
    <technology>[Tech stack/tools]</technology>
    <constraints>[Limitations]</constraints>
  </resources>
</strategy_development>

Develop a comprehensive strategy including:
1. Executive summary
2. SWOT analysis
3. Strategic objectives (SMART goals)
4. Key initiatives with priorities
5. Resource allocation plan
6. Timeline with milestones
7. Success metrics/KPIs
8. Risk mitigation plan
9. Communication strategy
10. Quick wins for momentum
```

### 9. Data Visualization Planning
```python
dataviz_template = """
Plan a data visualization for this dataset:

<dataset>
  <description>[What the data represents]</description>
  <fields>
    - [Field 1]: [type, range, description]
    - [Field 2]: [type, range, description]
    - [Field 3]: [type, range, description]
  </fields>
  <size>[Number of records]</size>
  <update_frequency>[Static|Daily|Real-time]</update_frequency>
</dataset>

<audience>
  <technical_level>[High|Medium|Low]</technical_level>
  <familiarity>[Expert|Familiar|New to topic]</familiarity>
  <needs>[What they need to understand]</needs>
</audience>

<goals>
  - [Primary insight to convey]
  - [Secondary insights]
  - [Actions to enable]
</goals>

Create a visualization plan:
<visualization_plan>
  <chart_type>
    Recommend best chart type with justification
  </chart_type>
  
  <visual_encoding>
    - X-axis: [Field and reason]
    - Y-axis: [Field and reason]
    - Color: [Field and reason]
    - Size: [Field and reason]
    - Other encodings: [If applicable]
  </visual_encoding>
  
  <interactivity>
    - Hover details
    - Filtering options
    - Drill-down capabilities
    - Animation (if applicable)
  </interactivity>
  
  <layout>
    - Dashboard structure
    - Supporting elements
    - Annotations needed
  </layout>
  
  <implementation>
    - Tool recommendation
    - Code structure
    - Performance considerations
  </implementation>
</visualization_plan>
"""
```

### 10. Research Paper Analysis
```xml
<paper_analysis>
  <paper_details>
    <title>[Paper title]</title>
    <authors>[Author list]</authors>
    <venue>[Journal/Conference]</venue>
    <year>[Publication year]</year>
    <field>[Research field]</field>
  </paper_details>
  
  <content>
    [Insert abstract or full paper text]
  </content>
  
  <analysis_requirements>
    - Summarize key contributions
    - Evaluate methodology
    - Assess evidence quality
    - Identify limitations
    - Compare to related work
    - Extract practical applications
    - Suggest follow-up research
  </analysis_requirements>
</paper_analysis>

Provide structured analysis:
<analysis>
  <summary>
    One paragraph capturing essence
  </summary>
  
  <contributions>
    1. [Main contribution]
    2. [Secondary contribution]
  </contributions>
  
  <methodology>
    <approach>[Description]</approach>
    <strengths>[What works well]</strengths>
    <weaknesses>[Limitations]</weaknesses>
  </methodology>
  
  <results>
    <key_findings>[Main results]</key_findings>
    <statistical_significance>[If applicable]</statistical_significance>
    <practical_impact>[Real-world relevance]</practical_impact>
  </results>
  
  <critical_assessment>
    <validity>[Assessment of claims]</validity>
    <reproducibility>[Can it be reproduced]</reproducibility>
    <generalizability>[How broadly applicable]</generalizability>
  </critical_assessment>
  
  <implications>
    <theoretical>[Advances to field]</theoretical>
    <practical>[Applications]</practical>
    <future_work>[Research directions]</future_work>
  </implications>
</analysis>
```

## Usage Tips

1. **Customization**: Replace placeholder text in [brackets] with your specific content
2. **XML Tags**: Claude responds exceptionally well to XML structure - maintain it where present
3. **Length**: Adjust detail level based on your needs - these templates are comprehensive starting points
4. **Combination**: Mix and match sections from different templates for hybrid use cases
5. **Iteration**: Use results from one template as input for another for complex workflows

## Best Practices

- Always provide context about your specific situation
- Be explicit about output format preferences
- Include examples when possible
- Specify any constraints or limitations
- Request confidence levels for critical decisions
- Ask for alternative approaches when applicable

---

*These templates represent proven patterns optimized for Claude's capabilities. Adapt and evolve them based on your specific needs.*
