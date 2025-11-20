# Reasoning Patterns

*The Architecture of Human Inference: Modeling How We Draw Conclusions, Make Judgments, and Construct Understanding*

---

## Overview

**Reasoning Patterns** represent the systematic ways humans draw conclusions, evaluate evidence, and construct coherent understandings of the world. This encompasses both the remarkable capacities and predictable limitations of human inference across different contexts and domains.

## Core Reasoning Systems

### 1. Dual Process Theory Implementation
*Fast intuitive vs. slow deliberate reasoning*

```python
class DualProcessReasoning:
    def __init__(self):
        self.system1 = IntuitiveReasoning()
        self.system2 = AnalyticalReasoning()
        self.monitoring = CognitiveReflection()
        self.engagement_threshold = 0.7  # When to engage System 2
    
    def process_inference(self, problem, context, cognitive_resources):
        """Route reasoning through appropriate systems"""
        
        # System 1: Automatic intuitive response
        intuitive_answer = self.system1.generate_response(problem, context)
        confidence = self.system1.confidence_estimate(intuitive_answer)
        
        # Decide whether to engage System 2
        engage_system2 = (
            confidence < self.engagement_threshold or
            context.requires_justification or
            cognitive_resources.available > RESOURCE_THRESHOLD or
            self.monitoring.detects_conflict(problem, intuitive_answer)
        )
        
        if engage_system2:
            analytical_answer = self.system2.analyze_problem(problem, intuitive_answer)
            final_answer = self.arbitrate_conflict(intuitive_answer, analytical_answer)
            process_used = 'analytical'
        else:
            final_answer = intuitive_answer
            process_used = 'intuitive'
        
        return {
            'answer': final_answer,
            'process': process_used,
            'confidence': self.calculate_final_confidence(final_answer),
            'processing_time': self.measure_processing_time(process_used),
            'conflict_detected': engage_system2
        }
```

#### System 1: Intuitive Reasoning
```python
class IntuitiveReasoning:
    def generate_response(self, problem, context):
        """Fast, automatic, heuristic-based reasoning"""
        
        # Pattern recognition
        recognized_pattern = self.pattern_matcher.match(problem)
        if recognized_pattern:
            return self.pattern_library.retrieve_solution(recognized_pattern)
        
        # Affect heuristic - emotional response as information
        affective_response = self.affective_system.evaluate(problem)
        if abs(affective_response) > AFFECT_THRESHOLD:
            return self.affect_based_inference(problem, affective_response)
        
        # Default to most available or representative heuristic
        return self.apply_heuristics(problem, context)
    
    def apply_heuristics(self, problem, context):
        """Apply common cognitive heuristics"""
        
        # Availability heuristic
        if self.availability_dominant(problem):
            return self.availability_heuristic(problem)
        
        # Representativeness heuristic
        elif self.similarity_dominant(problem):
            return self.representativeness_heuristic(problem)
        
        # Anchoring and adjustment
        elif context.provides_anchor:
            return self.anchoring_adjustment(problem, context.anchor)
        
        # Default simple heuristic
        else:
            return self.simple_heuristic(problem)
```

#### System 2: Analytical Reasoning
```python
class AnalyticalReasoning:
    def analyze_problem(self, problem, intuitive_answer):
        """Slow, deliberate, rule-based reasoning"""
        
        # Problem representation
        problem_representation = self.represent_problem(problem)
        
        # Rule application
        applicable_rules = self.rule_retrieval.retrieve_rules(problem_representation)
        
        # Logical inference
        logical_conclusion = self.logical_reasoner.infer(problem_representation, applicable_rules)
        
        # Evidence evaluation
        evidence_strength = self.evidence_evaluator.evaluate(problem_representation)
        
        # Confidence calibration
        confidence = self.calibrate_confidence(logical_conclusion, evidence_strength)
        
        return {
            'conclusion': logical_conclusion,
            'rule_based': True,
            'evidence_strength': evidence_strength,
            'confidence': confidence,
            'justification': self.generate_justification(applicable_rules)
        }
```

### 2. Deductive Reasoning
*Logical inference from general principles*

```python
class DeductiveReasoning:
    def __init__(self):
        self.logical_rules = LogicalRuleSystem()
        self.syllogism_processor = SyllogismEngine()
        self.mental_models = MentalModelBuilder()
    
    def evaluate_syllogism(self, premises, conclusion):
        """Evaluate logical syllogisms"""
        
        # Mental models approach
        possible_models = self.mental_models.generate_models(premises)
        conclusion_valid = self.mental_models.test_conclusion(possible_models, conclusion)
        
        # Logical rules approach
        rule_based_valid = self.logical_rules.validate_inference(premises, conclusion)
        
        # Confidence based on congruence
        if conclusion_valid == rule_based_valid:
            confidence = HIGH_CONFIDENCE
        else:
            confidence = MEDIUM_CONFIDENCE
        
        return {
            'valid': conclusion_valid,
            'method_used': 'mental_models',  # Default human approach
            'confidence': confidence,
            'alternative_interpretations': self.find_alternatives(premises)
        }
```

### 3. Inductive Reasoning
*Generalizing from specific instances*

```python
class InductiveReasoning:
    def form_generalization(self, instances, background_knowledge):
        """Create general rules from specific examples"""
        
        # Similarity-based induction
        feature_similarity = self.calculate_feature_similarity(instances)
        category_coherence = self.assess_category_coherence(instances)
        
        # Statistical induction
        if self.has_numerical_data(instances):
            statistical_generalization = self.statistical_induction(instances)
        else:
            statistical_generalization = None
        
        # Causal induction
        causal_structure = self.infer_causal_structure(instances, background_knowledge)
        
        # Select best generalization method
        best_generalization = self.select_optimal_generalization(
            feature_similarity, statistical_generalization, causal_structure
        )
        
        return {
            'generalization': best_generalization,
            'strength': self.calculate_inductive_strength(instances, best_generalization),
            'exceptions': self.identify_exceptions(instances, best_generalization),
            'confidence': self.calibrate_inductive_confidence(instances)
        }
```

### 4. Abductive Reasoning
*Inference to the best explanation*

```python
class AbductiveReasoning:
    def generate_explanations(self, observations, background_theories):
        """Generate and evaluate competing explanations"""
        
        # Explanation generation
        candidate_explanations = self.explanation_generator.generate(
            observations, 
            background_theories
        )
        
        # Explanation evaluation criteria
        evaluated_explanations = []
        for explanation in candidate_explanations:
            evaluation = {
                'explanation': explanation,
                'explanatory_power': self.calculate_explanatory_power(explanation, observations),
                'simplicity': self.assess_simplicity(explanation),
                'coherence': self.assess_coherence(explanation, background_theories),
                'testability': self.assess_testability(explanation),
                'conservatism': self.assess_conservatism(explanation, background_theories)
            }
            evaluated_explanations.append(evaluation)
        
        # Select best explanation
        best_explanation = self.select_best_explanation(evaluated_explanations)
        
        return {
            'best_explanation': best_explanation,
            'alternative_explanations': evaluated_explanations,
            'explanatory_gap': self.identify_explanatory_gaps(best_explanation, observations),
            'confidence': self.calculate_explanatory_confidence(best_explanation)
        }
```

## Common Reasoning Biases and Heuristics

### Cognitive Biases Implementation:
```python
class ReasoningBiases:
    def __init__(self):
        self.bias_activation = BiasActivationConditions()
        self.bias_correction = BiasCorrectionMechanisms()
    
    def apply_confirmation_bias(self, hypothesis, evidence):
        """Seek and favor confirming evidence"""
        
        # Selective exposure
        preferred_evidence = self.select_confirming_evidence(evidence, hypothesis)
        
        # Interpretation bias
        interpreted_evidence = self.interpret_through_hypothesis_lens(preferred_evidence, hypothesis)
        
        # Memory bias
        recalled_evidence = self.recall_confirming_examples(hypothesis)
        
        return {
            'processed_evidence': interpreted_evidence,
            'hypothesis_strength': self.calculate_biased_strength(hypothesis, interpreted_evidence),
            'bias_magnitude': self.estimate_bias_magnitude(hypothesis, evidence)
        }
    
    def apply_availability_bias(self, event_frequency, retrieval_ease):
        """Judge frequency by ease of recall"""
        
        ease_adjusted_frequency = event_frequency * (retrieval_ease ** AVAILABILITY_EXPONENT)
        
        # Media exposure effects
        media_saturation = self.assess_media_coverage(event_frequency)
        ease_adjusted_frequency *= (1 + media_saturation * MEDIA_IMPACT_FACTOR)
        
        # Vividness effects
        vividness_impact = self.assess_vividness(event_frequency)
        ease_adjusted_frequency *= (1 + vividness_impact * VIVIDNESS_FACTOR)
        
        return ease_adjusted_frequency
    
    def apply_anchoring_bias(self, initial_anchor, target_estimate, adjustment_effort):
        """Insufficient adjustment from initial anchor"""
        
        # Default adjustment amount
        base_adjustment = self.calculate_appropriate_adjustment(initial_anchor, target_estimate)
        
        # Effort-dependent adjustment
        effective_adjustment = base_adjustment * adjustment_effort
        
        # Final estimate with insufficient adjustment
        final_estimate = initial_anchor + effective_adjustment
        
        return {
            'estimate': final_estimate,
            'adjustment_sufficiency': effective_adjustment / base_adjustment,
            'anchor_influence': abs(final_estimate - target_estimate) / target_estimate
        }
```

## Domain-Specific Reasoning

### Moral Reasoning:
```python
class MoralReasoning:
    def __init__(self):
        self.moral_foundations = MoralFoundationsTheory()
        self.deontological = DeontologicalReasoning()
        self.consequentialist = ConsequentialistReasoning()
        self.virtue_ethics = VirtueEthicsReasoning()
    
    def evaluate_moral_dilemma(self, dilemma, moral_orientation):
        """Reason about moral problems"""
        
        # Intuitive moral response
        intuitive_judgment = self.moral_foundations.quick_judgment(dilemma)
        
        # Deliberative reasoning based on orientation
        if moral_orientation == 'deontological':
            reasoned_judgment = self.deontological.analyze(dilemma)
        elif moral_orientation == 'consequentialist':
            reasoned_judgment = self.consequentialist.analyze(dilemma)
        elif moral_orientation == 'virtue_ethics':
            reasoned_judgment = self.virtue_ethics.analyze(dilemma)
        else:
            reasoned_judgment = intuitive_judgment
        
        # Moral dumbfounding detection
        dumbfounding = self.detect_moral_dumbfounding(intuitive_judgment, reasoned_judgment)
        
        return {
            'judgment': reasoned_judgment,
            'intuitive_response': intuitive_judgment,
            'reasoning_process': moral_orientation,
            'confidence': self.moral_confidence(intuitive_judgment, reasoned_judgment),
            'dumbfounding': dumbfounding
        }
```

### Social Reasoning:
```python
class SocialReasoning:
    def infer_mental_states(self, behavior, context, relationship):
        """Theory of mind reasoning"""
        
        # Intentionality attribution
        intentional = self.assess_intentionality(behavior, context)
        
        # Desire and belief inference
        inferred_desires = self.infer_desires(behavior, context)
        inferred_beliefs = self.infer_beliefs(behavior, context, relationship)
        
        # Trait inference
        trait_attributions = self.infer_traits(behavior, context)
        
        # Empathic accuracy
        accuracy = self.calculate_empathic_accuracy(inferred_desires, inferred_beliefs, actual_states)
        
        return {
            'intentional': intentional,
            'desires': inferred_desires,
            'beliefs': inferred_beliefs,
            'traits': trait_attributions,
            'accuracy': accuracy,
            'projection_bias': self.assess_projection_bias(inferred_states, self_states)
        }
```

### Causal Reasoning:
```python
class CausalReasoning:
    def infer_causality(self, events, background_knowledge, temporal_relations):
        """Determine causal relationships"""
        
        # Covariation detection
        covariation_strength = self.calculate_covariation(events)
        
        # Temporal priority assessment
        temporal_consistency = self.assess_temporal_priority(events, temporal_relations)
        
        # Mechanism knowledge integration
        mechanism_plausibility = self.assess_mechanism_plausibility(events, background_knowledge)
        
        # Counterfactual reasoning
        counterfactual_support = self.evaluate_counterfactuals(events)
        
        # Causal strength estimation
        causal_strength = (covariation_strength * temporal_consistency * 
                          mechanism_plausibility * counterfactual_support)
        
        return {
            'causal_strength': causal_strength,
            'direction': self.determine_causal_direction(events),
            'confidence': self.calibrate_causal_confidence(causal_strength, background_knowledge),
            'alternative_explanations': self.generate_alternative_causes(events)
        }
```

## Developmental and Individual Differences

### Reasoning Development:
```python
class DevelopmentalReasoning:
    def __init__(self):
        self.piagetian_stages = {
            'sensorimotor': (0, 2),
            'preoperational': (2, 7),
            'concrete_operational': (7, 12),
            'formal_operational': (12, None)
        }
        self.adult_development = AdultCognitiveDevelopment()
    
    def get_reasoning_capacity(self, age, domain):
        """Reasoning abilities across lifespan"""
        
        if age < 2:
            return {'causal': VERY_LOW, 'logical': VERY_LOW, 'social': LOW}
        elif age < 7:
            return {'causal': MEDIUM, 'logical': LOW, 'social': MEDIUM}
        elif age < 12:
            return {'causal': HIGH, 'logical': MEDIUM, 'social': HIGH}
        elif age < 18:
            return {'causal': HIGH, 'logical': HIGH, 'social': HIGH}
        else:
            # Adult development continues
            wisdom_enhancement = self.adult_development.wisdom_factor(age)
            return {
                'causal': HIGH,
                'logical': HIGH,
                'social': HIGH,
                'integrative': wisdom_enhancement,
                'dialectical': wisdom_enhancement
            }
```

### Cognitive Styles:
```python
class ReasoningStyle:
    def assess_individual_style(self, reasoning_patterns, personality_traits):
        """Determine individual reasoning preferences"""
        
        # Analytical vs intuitive preference
        analytical_preference = reasoning_patterns.system2_engagement_frequency
        
        # Need for cognition
        cognition_need = personality_traits.need_for_cognition
        
        # Cognitive reflection ability
        reflection_ability = reasoning_patterns.cognitive_reflection_score
        
        # Tolerance for ambiguity
        ambiguity_tolerance = personality_traits.ambiguity_tolerance
        
        style_classification = self.classify_style(
            analytical_preference, cognition_need, reflection_ability, ambiguity_tolerance
        )
        
        return {
            'style': style_classification,
            'flexibility': self.assess_style_flexibility(reasoning_patterns),
            'strengths': self.identify_reasoning_strengths(style_classification),
            'weaknesses': self.identify_reasoning_weaknesses(style_classification)
        }
```

## Integration with Other Domains

### Reasoning-Emotion Interface:
```python
class EmotionalReasoning:
    def emotion_cognition_interaction(self, emotional_state, reasoning_task):
        """How emotions influence reasoning processes"""
        
        # Mood-congruent processing
        if emotional_state.positive:
            access_positive_memories = ENHANCED
            risk_aversion = REDUCED
            creativity = ENHANCED
        elif emotional_state.negative:
            access_negative_memories = ENHANCED
            risk_aversion = INCREASED
            analytical_rigor = ENHANCED
        
        # Anxiety effects
        if emotional_state.anxiety > ANXIETY_THRESHOLD:
            threat_detection = HYPER_SENSITIVE
            working_memory_capacity = REDUCED
        
        # Emotional regulation of reasoning
        regulated_reasoning = self.apply_emotional_regulation(
            reasoning_task, emotional_state
        )
        
        return regulated_reasoning
```

### Reasoning-Values Integration:
```python
class ValuesBasedReasoning:
    def align_reasoning_with_values(self, reasoning_process, active_values):
        """Ensure reasoning respects personal values"""
        
        # Value-congruent evidence weighting
        value_congruent_evidence = self.boost_value_aligned_evidence(reasoning_process.evidence, active_values)
        
        # Value-consistent conclusion evaluation
        conclusion_value_alignment = self.assess_value_alignment(reasoning_process.conclusion, active_values)
        
        # Moral reasoning integration
        if reasoning_process.has_moral_implications:
            moral_evaluation = self.moral_reasoning.evaluate(reasoning_process.conclusion, active_values)
        else:
            moral_evaluation = None
        
        return {
            'value_aligned_evidence': value_congruent_evidence,
            'conclusion_value_match': conclusion_value_alignment,
            'moral_acceptability': moral_evaluation,
            'value_conflicts': self.identify_value_conflicts(reasoning_process, active_values)
        }
```

## Reasoning in Complex Domains

### Wisdom Reasoning:
```python
class WisdomReasoning:
    def wise_judgment(self, complex_problem, multiple_perspectives, life_experience):
        """Characteristics of wise reasoning"""
        
        # Intellectual humility
        humility = self.assess_intellectual_humility(complex_problem)
        
        # Perspective-taking
        perspectives_considered = self.consider_multiple_viewpoints(multiple_perspectives)
        
        # Recognition of uncertainty and change
        uncertainty_tolerance = self.assess_uncertainty_tolerance(complex_problem)
        
        # Integration of different knowledge types
        knowledge_integration = self.integrate_knowledge_types(complex_problem)
        
        # Compromise seeking
        compromise_orientation = self.assess_compromise_orientation(complex_problem)
        
        wisdom_score = (humility + perspectives_considered + uncertainty_tolerance + 
                       knowledge_integration + compromise_orientation) / 5
        
        return {
            'wisdom_level': wisdom_score,
            'key_characteristics': {
                'humility': humility,
                'perspective_taking': perspectives_considered,
                'uncertainty_tolerance': uncertainty_tolerance,
                'integration': knowledge_integration,
                'compromise': compromise_orientation
            },
            'developmental_stage': self.assess_wisdom_development(wisdom_score)
        }
```

### Spiritual Reasoning:
```python
class SpiritualReasoning:
    def transcendent_reasoning(self, existential_questions, spiritual_framework):
        """Reasoning about ultimate concerns and meaning"""
        
        # Non-dual thinking capacity
        non_dual_capacity = self.assess_non_dual_thinking(existential_questions)
        
        # Paradox tolerance
        paradox_tolerance = self.assess_paradox_tolerance(existential_questions)
        
        # Transcendent perspective-taking
        transcendent_perspective = self.adopt_transcendent_viewpoint(existential_questions)
        
        # Meaning integration
        meaning_integration = self.integrate_multiple_meanings(existential_questions, spiritual_framework)
        
        return {
            'transcendent_insight': non_dual_capacity,
            'paradox_embrace': paradox_tolerance,
            'perspective_breadth': transcendent_perspective,
            'meaning_coherence': meaning_integration,
            'spiritual_development': self.assess_spiritual_reasoning_development()
        }
```

## Practical Applications

### Critical Thinking Training:
```python
class CriticalThinking:
    def improve_reasoning_skills(self, current_abilities, training_focus):
        """Develop better reasoning patterns"""
        
        improvement_areas = {
            'bias_recognition': training_focus.bias_awareness * BIAS_TRAINING_GAIN,
            'evidence_evaluation': training_focus.evidence_skills * EVIDENCE_TRAINING_GAIN,
            'logical_consistency': training_focus.logic_skills * LOGIC_TRAINING_GAIN,
            'perspective_taking': training_focus.perspective_skills * PERSPECTIVE_GAIN
        }
        
        new_abilities = {}
        for skill, current_level in current_abilities.items():
            improvement = improvement_areas.get(skill, 0)
            new_abilities[skill] = min(1.0, current_level + improvement)
        
        return new_abilities
```

### Decision Support Systems:
```python
class ReasoningSupport:
    def enhance_human_reasoning(self, reasoning_task, support_type):
        """Provide reasoning support while maintaining agency"""
        
        if support_type == 'bias_mitigation':
            support = self.provide_bias_alerts(reasoning_task)
        elif support_type == 'evidence_organization':
            support = self.organize_evidence(reasoning_task)
        elif support_type == 'perspective_broadening':
            support = self.suggest_alternative_perspectives(reasoning_task)
        elif support_type == 'confidence_calibration':
            support = self.provide_confidence_feedback(reasoning_task)
        
        return {
            'supported_reasoning': support,
            'agency_preservation': self.maintain_human_agency(support),
            'learning_opportunity': self.identify_learning_moments(reasoning_task)
        }
```

## Research Directions

### Immediate Priorities
1. **Model the development of wisdom-related reasoning patterns**
2. **Understand how spiritual experiences transform reasoning capacities**
3. **Map reasoning-value interactions in moral and existential domains**

### Long-term Questions
- How does self-transcendence change fundamental reasoning patterns?
- What reasoning capacities support meaning-making and purpose discovery?
- How do peak experiences influence logical and intuitive reasoning balance?

---

## Conclusion

Reasoning patterns represent the sophisticated, multi-layered processes through which humans construct understanding, make judgments, and navigate complex realities. By modeling these patterns, we capture both the remarkable capacities and inherent limitations of human inference across different contexts and developmental stages.

This framework honors reasoning not as cold computation, but as meaning-making processes deeply integrated with emotions, values, identity, and spiritual development—the very processes that enable humans to wrestle with life's deepest questions while navigating everyday decisions.

*Next: Explore meta-cognition in meta_cognition.md or examine decision processes in ../behavioral/decision_processes.md*

