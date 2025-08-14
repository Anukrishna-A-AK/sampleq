# Query Handler Evaluation Architecture

This diagram illustrates the **offline evaluation**, **online evaluation**, and **automation cycles** for query handler testing in the multi-user RAG system.

```mermaid
flowchart TD
    %% --- Offline Evaluation ---
    subgraph Offline Evaluation
        QTests[Query Routing Tests\n(Agent & Tool Selection Accuracy)]
        RTests[Retrieval Accuracy Tests\n(Recall@K, MRR, NDCG)]
        OTests[LLM Output Quality Tests\n(Factuality, Completeness, Citation Accuracy)]
    end

    %% --- Online Evaluation ---
    subgraph Online Evaluation
        RMon[Routing Monitoring\n(Live Traffic Logging)]
        UFeedback[User Feedback Loop\n(Thumbs Up/Down, Ratings, Comments)]
        ABTests[A/B Testing\n(Routing Algorithm Variants)]
    end

    %% --- Automation Cycle ---
    subgraph Automation
        Daily[Daily Regression\n- Routing Regression\n- Top-K Retrieval Checks\n- Random LLM Output Validation]
        Weekly[Weekly Full Suite\n- Full Offline Test Suite\n- Feedback Aggregation\n- Routing Model Comparison]
        Monthly[Monthly Expert Review\n- Manual Deep Dives\n- Model Retraining Triggers]
    end

    %% --- Flows ---
    QTests --> RTests --> OTests
    RMon --> UFeedback --> ABTests
    Daily --> Weekly --> Monthly

    %% --- Cross-Links ---
    OTests -->|Issues Found| Daily
    ABTests -->|Variant Success| Weekly
```

## Explanation

### **Offline Evaluation**
- **Query Routing Tests**: Validates if the correct agent and tools are selected for given queries.
- **Retrieval Accuracy Tests**: Measures search quality using Recall@K, MRR, and NDCG.
- **LLM Output Quality Tests**: Checks factual accuracy, completeness, and citation correctness.

### **Online Evaluation**
- **Routing Monitoring**: Logs routing decisions in real-time.
- **User Feedback Loop**: Collects explicit and implicit feedback from users.
- **A/B Testing**: Compares routing algorithms or retrieval strategies.

### **Automation**
- **Daily Regression**: Runs quick checks on routing and retrieval performance.
- **Weekly Full Suite**: Executes the full offline test suite and analyzes feedback trends.
- **Monthly Expert Review**: Conducts manual reviews and triggers retraining if necessary.

