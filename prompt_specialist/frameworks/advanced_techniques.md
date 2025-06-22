# Advanced Prompt Engineering Techniques

## Meta-Cognitive Patterns

### The Self-Evaluation Pattern
Forces the model to assess its own reasoning:

```xml
<task>
  <instruction>[Your main task]</instruction>
  
  <metacognition>
    Before providing your final answer:
    1. List your assumptions
    2. Identify potential biases
    3. Consider alternative perspectives
    4. Rate your confidence (1-10) with justification
  </metacognition>
  
  <output>
    <reasoning>[Step-by-step thought process]</reasoning>
    <assumptions>[List key assumptions]</assumptions>
    <alternatives>[Other valid approaches]</alternatives>
    <confidence>[Score and explanation]</confidence>
    <answer>[Final response]</answer>
  </output>
</task>
```

### The Recursive Refinement Pattern
Iteratively improves output quality:

```python
recursive_prompt = """
Generate a {output_type} for {topic}.

After your initial draft:
1. Critique your own work identifying weaknesses
2. Suggest 3 specific improvements
3. Implement those improvements in a revised version
4. Explain what changed and why

<iteration_1>
[Initial draft]
</iteration_1>

<critique>
[Self-critique]
</critique>

<iteration_2>
[Improved version]
</iteration_2>

<changes>
[Explanation of improvements]
</changes>
"""
```

## Complex Reasoning Techniques

### Tree-of-Thought Pattern
Explores multiple reasoning paths:

```xml
<tree_of_thought>
  <problem>[Problem statement]</problem>
  
  <initial_thoughts>
    <thought_1>
      <approach>[First approach]</approach>
      <viability>[High/Medium/Low]</viability>
    </thought_1>
    <thought_2>
      <approach>[Second approach]</approach>
      <viability>[High/Medium/Low]</viability>
    </thought_2>
    <thought_3>
      <approach>[Third approach]</approach>
      <viability>[High/Medium/Low]</viability>
    </thought_3>
  </initial_thoughts>
  
  <exploration>
    <!-- For each viable thought -->
    <branch thought="1">
      <step_1>[First step in this approach]</step_1>
      <step_2>[Second step]</step_2>
      <outcome>[Predicted result]</outcome>
      <rating>[Success likelihood]</rating>
    </branch>
  </exploration>
  
  <best_path>
    [Selected approach with justification]
  </best_path>
</tree_of_thought>
```

### Least-to-Most Prompting
Builds understanding progressively:

```python
def least_to_most_prompt(complex_problem):
    progressive_prompt = f"""
We'll solve this step-by-step, building complexity gradually:

Problem: {complex_problem}

Step 1: Understanding Basic Concepts
<basic_concepts>
[Explain fundamental concepts involved]
</basic_concepts>

Step 2: Identifying Relationships
<relationships>
[Map connections between concepts]
</relationships>

Step 3: Solving Simple Case
<simple_case>
[Solve simplified version of the problem]
</simple_case>

Step 4: Applying to Full Problem
<full_solution>
[Apply learning to complete problem]
</full_solution>
"""
    return progressive_prompt
```

### Analogical Reasoning Pattern
Leverages similar problems for insight:

```python
analogical_prompt = """
I need to solve: {target_problem}

First, identify 3 analogous problems from different domains:

<analogies>
  <analogy domain="{domain1}">
    <problem>[Similar problem in this domain]</problem>
    <solution>[How it's solved]</solution>
    <key_insight>[Transferable principle]</key_insight>
  </analogy>
  <analogy domain="{domain2}">
    <problem>[Similar problem in this domain]</problem>
    <solution>[How it's solved]</solution>
    <key_insight>[Transferable principle]</key_insight>
  </analogy>
  <analogy domain="{domain3}">
    <problem>[Similar problem in this domain]</problem>
    <solution>[How it's solved]</solution>
    <key_insight>[Transferable principle]</key_insight>
  </analogy>
</analogies>

<mapping>
  Map the insights from analogies to our target problem:
  - From {domain1}: [How insight applies]
  - From {domain2}: [How insight applies]
  - From {domain3}: [How insight applies]
</mapping>

<novel_solution>
  Combining these insights, here's the solution:
  [Synthesized approach]
</novel_solution>
"""
```

## Perspective Analysis Patterns

### The Perspective Matrix Pattern
Analyzes problems from multiple viewpoints:

```xml
<analysis_matrix>
  <topic>[Subject for analysis]</topic>
  
  <perspectives>
    <technical>
      <pros>[Technical advantages]</pros>
      <cons>[Technical challenges]</cons>
      <verdict>[Technical assessment]</verdict>
    </technical>
    
    <business>
      <pros>[Business benefits]</pros>
      <cons>[Business risks]</cons>
      <verdict>[Business viability]</verdict>
    </business>
    
    <user>
      <pros>[User advantages]</pros>
      <cons>[User pain points]</cons>
      <verdict>[User acceptance likelihood]</verdict>
    </user>
    
    <ethical>
      <pros>[Ethical benefits]</pros>
      <cons>[Ethical concerns]</cons>
      <verdict>[Ethical recommendation]</verdict>
    </ethical>
  </perspectives>
  
  <synthesis>
    [Balanced final recommendation considering all perspectives]
  </synthesis>
</analysis_matrix>
```

### Stakeholder Analysis Pattern
```xml
<stakeholder_analysis>
  <decision>[Decision or change being considered]</decision>
  
  <stakeholders>
    <stakeholder>
      <name>[Stakeholder group]</name>
      <interests>[What they care about]</interests>
      <impact>[How this affects them]</impact>
      <influence>[Their power to affect outcome]</influence>
      <concerns>[Likely objections]</concerns>
      <benefits>[What they gain]</benefits>
    </stakeholder>
    <!-- Repeat for each stakeholder -->
  </stakeholders>
  
  <strategy>
    <communication>[How to communicate with each group]</communication>
    <mitigation>[How to address concerns]</mitigation>
    <engagement>[How to involve them in process]</engagement>
  </strategy>
</stakeholder_analysis>
```

## Problem Decomposition Techniques

### Structured Decomposition Pattern
Breaks complex problems into manageable components:

```python
decomposition_template = """
Complex Problem: {problem_statement}

<decomposition>
  <core_challenge>
    [Identify the fundamental challenge]
  </core_challenge>
  
  <subproblems>
    <subproblem id="1">
      <description>[Description]</description>
      <dependencies>[Other subproblems this depends on]</dependencies>
      <solution_approach>[How to solve]</solution_approach>
      <complexity>[High/Medium/Low]</complexity>
    </subproblem>
    <subproblem id="2">
      <description>[Description]</description>
      <dependencies>[Other subproblems this depends on]</dependencies>
      <solution_approach>[How to solve]</solution_approach>
      <complexity>[High/Medium/Low]</complexity>
    </subproblem>
    <!-- Continue for all subproblems -->
  </subproblems>
  
  <solution_sequence>
    1. [First step with subproblem IDs]
    2. [Second step with subproblem IDs]
    3. [Continue sequence]
  </solution_sequence>
  
  <integration>
    [How to combine subproblem solutions into final solution]
  </integration>
</decomposition>
"""
```

### Root Cause Analysis Pattern
```xml
<root_cause_analysis>
  <problem>[Problem description]</problem>
  
  <symptoms>
    - [Observable symptom 1]
    - [Observable symptom 2]
    - [Observable symptom 3]
  </symptoms>
  
  <five_whys>
    <why_1>
      <question>Why does [problem] occur?</question>
      <answer>[First level cause]</answer>
    </why_1>
    <why_2>
      <question>Why does [first level cause] happen?</question>
      <answer>[Second level cause]</answer>
    </why_2>
    <!-- Continue to why_5 -->
  </five_whys>
  
  <contributing_factors>
    <factor category="process">[Process-related factor]</factor>
    <factor category="people">[Human factor]</factor>
    <factor category="technology">[Technical factor]</factor>
    <factor category="environment">[Environmental factor]</factor>
  </contributing_factors>
  
  <root_causes>
    <primary>[Main root cause]</primary>
    <secondary>[Contributing root causes]</secondary>
  </root_causes>
  
  <solutions>
    <immediate>[Quick fixes for symptoms]</immediate>
    <long_term>[Solutions addressing root causes]</long_term>
    <preventive>[Measures to prevent recurrence]</preventive>
  </solutions>
</root_cause_analysis>
```

## Creative Generation Techniques

### Constraint-Based Creativity
```xml
<creative_generation>
  <objective>[What you want to create]</objective>
  
  <constraints>
    <must_have>
      - [Required element 1]
      - [Required element 2]
    </must_have>
    <cannot_have>
      - [Forbidden element 1]
      - [Forbidden element 2]
    </cannot_have>
    <limitations>
      - [Resource constraint 1]
      - [Time constraint]
      - [Technical constraint]
    </limitations>
  </constraints>
  
  <inspiration_sources>
    - [Source 1: industry, nature, art, etc.]
    - [Source 2: different domain]
    - [Source 3: historical example]
  </inspiration_sources>
  
  <generation_process>
    1. Generate 10 initial ideas ignoring constraints
    2. Apply constraints to filter viable options
    3. Combine elements from different ideas
    4. Refine top 3 concepts
    5. Select best option with justification
  </generation_process>
</creative_generation>
```

### SCAMPER Technique
```xml
<scamper_analysis>
  <subject>[Thing to improve or modify]</subject>
  
  <substitute>
    What can be substituted? [Materials, processes, people, places]
  </substitute>
  
  <combine>
    What can be combined? [Ideas, purposes, units, appeals]
  </combine>
  
  <adapt>
    What can be adapted? [From other contexts, industries, time periods]
  </adapt>
  
  <modify>
    What can be modified? [Size, shape, color, motion, sound, smell]
  </modify>
  
  <put_to_other_uses>
    How else can this be used? [New ways, other markets, different contexts]
  </put_to_other_uses>
  
  <eliminate>
    What can be eliminated? [Parts, steps, rules, requirements]
  </eliminate>
  
  <reverse>
    What can be reversed? [Roles, order, layout, schedule]
  </reverse>
  
  <synthesis>
    [Best ideas from each category combined into novel solutions]
  </synthesis>
</scamper_analysis>
```

## Advanced Evaluation Techniques

### Multi-Criteria Decision Analysis
```xml
<mcda>
  <decision>[Decision to be made]</decision>
  
  <options>
    <option id="A">[Option A description]</option>
    <option id="B">[Option B description]</option>
    <option id="C">[Option C description]</option>
  </options>
  
  <criteria>
    <criterion weight="0.3">Cost effectiveness</criterion>
    <criterion weight="0.25">Implementation ease</criterion>
    <criterion weight="0.2">Strategic alignment</criterion>
    <criterion weight="0.15">Risk level</criterion>
    <criterion weight="0.1">Timeline</criterion>
  </criteria>
  
  <scoring>
    <!-- Score each option 1-10 on each criterion -->
    <option_scores id="A">
      <cost_effectiveness>8</cost_effectiveness>
      <implementation_ease>6</implementation_ease>
      <strategic_alignment>9</strategic_alignment>
      <risk_level>7</risk_level>
      <timeline>5</timeline>
    </option_scores>
    <!-- Repeat for other options -->
  </scoring>
  
  <calculation>
    [Weighted scores and final ranking]
  </calculation>
  
  <sensitivity_analysis>
    [How results change with different weightings]
  </sensitivity_analysis>
</mcda>
```

### Scenario Planning
```xml
<scenario_planning>
  <focal_question>[Key question about the future]</focal_question>
  
  <driving_forces>
    <force impact="high" uncertainty="high">[Force 1]</force>
    <force impact="high" uncertainty="medium">[Force 2]</force>
    <force impact="medium" uncertainty="high">[Force 3]</force>
  </driving_forces>
  
  <scenarios>
    <scenario name="Best Case">
      <description>[Optimistic scenario]</description>
      <key_assumptions>[What would need to be true]</key_assumptions>
      <implications>[What this means for decision]</implications>
      <probability>25%</probability>
    </scenario>
    
    <scenario name="Worst Case">
      <description>[Pessimistic scenario]</description>
      <key_assumptions>[What would need to be true]</key_assumptions>
      <implications>[What this means for decision]</implications>
      <probability>15%</probability>
    </scenario>
    
    <scenario name="Most Likely">
      <description>[Expected scenario]</description>
      <key_assumptions>[What would need to be true]</key_assumptions>
      <implications>[What this means for decision]</implications>
      <probability>45%</probability>
    </scenario>
    
    <scenario name="Wild Card">
      <description>[Unexpected scenario]</description>
      <key_assumptions>[What would need to be true]</key_assumptions>
      <implications>[What this means for decision]</implications>
      <probability>15%</probability>
    </scenario>
  </scenarios>
  
  <robust_strategies>
    [Strategies that work well across multiple scenarios]
  </robust_strategies>
</scenario_planning>
```

## Prompt Chaining Patterns

### Sequential Processing Chain
```python
chain_template = """
Step 1: Data Extraction
Extract key information from: {input_data}

<extraction>
[Structured data extraction]
</extraction>

Step 2: Analysis
Analyze the extracted data for: {analysis_focus}

<analysis>
[Detailed analysis based on extraction]
</analysis>

Step 3: Synthesis
Synthesize findings into: {output_format}

<synthesis>
[Final synthesized output]
</synthesis>
"""
```

### Parallel Processing Pattern
```xml
<parallel_analysis>
  <input>[Common input data]</input>
  
  <analysis_tracks>
    <track_1 focus="quantitative">
      [Numerical analysis approach]
    </track_1>
    
    <track_2 focus="qualitative">
      [Qualitative analysis approach]
    </track_2>
    
    <track_3 focus="comparative">
      [Comparative analysis approach]
    </track_3>
  </analysis_tracks>
  
  <integration>
    [Combine insights from all tracks]
  </integration>
</parallel_analysis>
```

## Error Handling & Validation

### Self-Validation Pattern
```xml
<task_with_validation>
  <primary_task>
    [Main task instructions]
  </primary_task>
  
  <validation_checks>
    After completing the primary task:
    1. Check logical consistency
    2. Verify all requirements met
    3. Identify potential errors
    4. Assess confidence level
    5. Suggest improvements
  </validation_checks>
  
  <output>
    <primary_response>[Main response]</primary_response>
    <validation_results>[Self-assessment]</validation_results>
    <confidence_score>[1-10 with justification]</confidence_score>
    <potential_improvements>[If any identified]</potential_improvements>
  </output>
</task_with_validation>
```

### Contradiction Detection
```xml
<contradiction_check>
  <statements>
    <statement_1>[First statement or claim]</statement_1>
    <statement_2>[Second statement or claim]</statement_2>
    <statement_3>[Third statement or claim]</statement_3>
  </statements>
  
  <analysis>
    <consistency_check>
      [Check for logical consistency between statements]
    </consistency_check>
    
    <contradictions>
      [Identify any contradictions with explanations]
    </contradictions>
    
    <resolution>
      [Suggest how to resolve contradictions]
    </resolution>
  </analysis>
</contradiction_check>
```

---

*These advanced techniques represent cutting-edge approaches to prompt engineering. Use them for complex reasoning tasks, creative problem-solving, and sophisticated analysis requirements.*
