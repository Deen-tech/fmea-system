# Architecture Notes

## Design principle

The system separates perception from decision-making:

- **Perception layer**: one LLM call extracts defect fields from unstructured inspection text.
- **Decision layer**: a deterministic Python rule engine calculates S/O/D scores and risk levels.
- **Human review layer**: high-risk or incomplete cases require an explicit `accept`, `reject`, or `modify` decision before persistence.

## Core flow

1. Inspection text is submitted to the API.
2. The LLM extracts structured defect information.
3. Schema validation and fallback parsing normalize the output.
4. The deterministic rule engine applies physical rules, expert rules, and case-based fallback logic.
5. Scoring evidence is attached to the result.
6. A review gate intercepts high-risk or incomplete cases.
7. Approved results are persisted and can be exported.

## Reliability mechanisms

- API-key middleware
- Database session isolation
- Celery and Redis task orchestration
- Review state handling
- Evidence-chain fields for traceability
- Failure paths that surface invalid or incomplete extraction

## Limitations

- Limited internal test set
- No external inspection-agency pilot
- No independent benchmark
- Management platform not included in this repository
- Production security and deployment hardening remain future work
