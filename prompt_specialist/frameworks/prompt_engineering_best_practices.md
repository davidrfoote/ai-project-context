# Prompt Engineering Best Practices & Core Principles

## The CLEAR Framework

A comprehensive framework for optimizing AI interactions:

- **Concise**: Use only essential words. Eliminate unnecessary language that could confuse the model.
- **Logical**: Structure prompts with intentional ordering of ideas to help Claude understand context and relationships.
- **Explicit**: Provide precise instructions about format, content, and scope of desired output.
- **Adaptive**: Refine prompts based on initial outputs, adding context or parameters as needed.
- **Reflective**: Critically evaluate AI responses and iterate on prompt design.

## Core Design Principles

### 1. Test-Driven Development
- Define success criteria before crafting prompts
- Create evaluation metrics for prompt performance
- Use A/B testing to compare prompt variants
- Iterate based on measurable results

### 2. Context Maximization
- Leverage Claude's 200k token window effectively
- Place important context early in the prompt
- Use data-first prompting (context before instructions)
- Structure information hierarchically

### 3. Structured Output
- Use XML tags for Claude prompts
- Employ JSON or markdown for other models
- Define clear output format requirements
- Include validation criteria

### 4. Progressive Complexity
- Start simple, add complexity as needed
- Use least-to-most prompting for complex tasks
- Break down multi-step problems
- Build understanding incrementally

## Claude-Specific Optimizations

### XML Structure Excellence
Claude responds exceptionally well to XML-structured prompts:

```xml
<task>
  <objective>Clear goal statement</objective>
  <context>Relevant background information</context>
  <requirements>
    <format>Expected output format</format>
    <length>Desired response length</length>
    <style>Tone and approach</style>
  </requirements>
</task>
```

### System Prompt Best Practices
- Use system parameter to set Claude's role
- Put task-specific instructions in user messages
- Keep system prompts focused on persona/behavior
- Avoid mixing role definition with task instructions

### Temperature Settings
- `0.0`: Deterministic, best for analysis and factual tasks
- `0.3-0.7`: Balanced creativity and consistency
- `0.8-1.0`: Maximum creativity, use for brainstorming

## Advanced Prompting Techniques

### 1. Chain-of-Thought (CoT) Prompting
Enhances reasoning by guiding models through step-by-step thinking:

**Basic CoT Pattern:**
```
[Task description]
Let's think step by step:
1. First, [break down the problem]
2. Then, [analyze components]
3. Finally, [synthesize solution]
```

**Zero-Shot CoT:**
Simply add: "Let's think step by step" to complex queries

### 2. Few-Shot Learning
- Provide 2-3 diverse, relevant examples
- Ensure examples mirror your actual use case
- More examples = better performance for complex tasks
- Use consistent formatting across examples

### 3. Meta-Cognitive Prompting
Force Claude to evaluate its own reasoning:

```xml
<metacognition>
Before providing your final answer:
1. List your assumptions
2. Identify potential biases
3. Consider alternative perspectives
4. Rate your confidence (1-10) with justification
</metacognition>
```

### 4. Role-Based Prompting
Leverage system prompts for domain expertise:

```
You are a senior financial analyst with 15 years of experience 
in tech industry valuations. You specialize in SaaS metrics and 
have a deep understanding of unit economics.
```

## Prompt Optimization Strategies

### Token Efficiency
- Remove redundant phrases ("Please", "Could you", "I would like")
- Use concise language without losing clarity
- Leverage Claude's understanding of context
- Optimize XML tag names (use short, clear tags)

### Error Prevention
- Include explicit constraints and limitations
- Define what NOT to do as well as what to do
- Add validation steps to the prompt
- Request confidence levels for critical outputs

### Output Quality Control
- Specify desired output structure explicitly
- Include examples of good vs. bad responses
- Request self-evaluation from the model
- Add quality checkpoints throughout complex tasks

## Common Patterns & Templates

### Analysis Pattern
```xml
<analyze>
  <data>[input data]</data>
  <method>[analytical approach]</method>
  <focus>[specific aspects to examine]</focus>
  <output>
    <summary>Key findings</summary>
    <details>In-depth analysis</details>
    <recommendations>Actionable next steps</recommendations>
  </output>
</analyze>
```

### Generation Pattern
```
Generate [type] that:
- Meets [specific criteria]
- Includes [required elements]
- Follows [style/format constraints]
- Avoids [things to exclude]

Format as: [specify exact output structure]
```

### Review Pattern
```
Review [subject] for:
1. [Evaluation criterion 1]
2. [Evaluation criterion 2]
3. [Evaluation criterion 3]

Provide feedback as:
- Issue: [description]
- Impact: [severity level]
- Solution: [specific recommendation]
```

## Evaluation & Testing

### Success Criteria Definition
Before crafting prompts, establish:
1. **Accuracy metrics**: What constitutes a correct response?
2. **Format compliance**: Does output match requirements?
3. **Completeness**: Are all requested elements included?
4. **Relevance**: Is the response on-topic and useful?

### Quality Metrics
- **Coherence**: Logical flow and consistency
- **Accuracy**: Factual correctness
- **Completeness**: All requirements addressed
- **Clarity**: Easy to understand
- **Actionability**: Practical and implementable

### A/B Testing Framework
```python
def test_prompt_variations(prompt_a, prompt_b, test_cases):
    results_a = []
    results_b = []
    
    for case in test_cases:
        response_a = get_completion(prompt_a.format(**case))
        results_a.append(evaluate_response(response_a))
        
        response_b = get_completion(prompt_b.format(**case))
        results_b.append(evaluate_response(response_b))
    
    return compare_results(results_a, results_b)
```

## Common Pitfalls & Solutions

### Pitfall 1: Vague Instructions
**Problem**: "Analyze this data"
**Solution**: "Analyze this sales data to identify trends, outliers, and growth opportunities. Provide specific recommendations with supporting evidence."

### Pitfall 2: Missing Context
**Problem**: Jumping straight to the task
**Solution**: Provide relevant background, constraints, and success criteria

### Pitfall 3: Unclear Output Format
**Problem**: No specification of desired response structure
**Solution**: Use XML tags or explicit formatting instructions

### Pitfall 4: Overloading Single Prompt
**Problem**: Trying to accomplish too much in one prompt
**Solution**: Break complex tasks into sequential prompts or use prompt chaining

### Pitfall 5: Ignoring Model Limitations
**Problem**: Asking for real-time data or capabilities the model doesn't have
**Solution**: Work within model constraints and be explicit about limitations

## Prompt Iteration Workflow

### 1. Initial Draft
- Start with basic requirements
- Use simple, clear language
- Include essential context only

### 2. Test & Evaluate
- Run prompt with sample inputs
- Measure against success criteria
- Identify failure modes

### 3. Refine & Optimize
- Add missing context or constraints
- Improve output format specifications
- Enhance clarity and specificity

### 4. Validate & Deploy
- Test with edge cases
- Confirm consistent performance
- Document final version and usage notes

## Best Practices Checklist

### Before Writing
- [ ] Define clear success criteria
- [ ] Identify target LLM and its strengths
- [ ] Gather relevant context and examples
- [ ] Plan output format and structure

### While Writing
- [ ] Use appropriate structure (XML for Claude)
- [ ] Place context before instructions
- [ ] Be explicit about requirements
- [ ] Include examples when helpful
- [ ] Specify output format clearly

### After Writing
- [ ] Test with sample inputs
- [ ] Evaluate against success criteria
- [ ] Check for edge cases
- [ ] Optimize for token efficiency
- [ ] Document usage guidelines

### Ongoing Optimization
- [ ] Monitor performance over time
- [ ] Collect user feedback
- [ ] A/B test improvements
- [ ] Update based on model changes
- [ ] Maintain version history

## Advanced Techniques

### Prompt Chaining
Link multiple prompts for complex workflows:
1. **Analysis prompt**: Extract key information
2. **Processing prompt**: Transform or analyze data
3. **Synthesis prompt**: Combine results into final output

### Conditional Logic
Use model reasoning for dynamic prompt paths:
```
If the data shows [condition], then focus on [approach A].
Otherwise, use [approach B].
```

### Self-Correction
Build error detection into prompts:
```
After generating your response:
1. Check for logical consistency
2. Verify all requirements are met
3. Identify any potential errors
4. Provide a corrected version if needed
```

### Meta-Prompting
Generate prompts for specific tasks:
```
Create an optimized prompt for [specific task] that:
- Uses Claude-specific best practices
- Includes appropriate structure and formatting
- Maximizes output quality for [specific goal]
```

---

*These best practices represent proven techniques for effective prompt engineering. Adapt and combine them based on your specific use cases and requirements.*
