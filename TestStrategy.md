1. Where the quality risk sits

 a. Flow: Payment and Checkout
    Services: Cart, Checkout, Payemnt, Currency, Recommendation, Email, Product Catalog
    Why: Monetory sensitive, user experience and compliance. PII data leakage.

 b. Flow: Fulfilment and Tracking
    Services: Accounting and Fraud Detection. Kafka Topics and events.
    Why: Back office is not visible to user, failures or frauds lead to order not delivered.
 
 c. Flow: Home Page, L1 Page Performance  
    Services: Product catalog, recommendations, ads, image provider, currency.
    Why: First customer interaction
 
 d. Accessibility Stale Serices/endpoints
    Services: Email, chatbot, excluding internal services.
    Why: Security exploitation, PII data leakage, bad practice.

2. The test pyramid

    a. Unit Testing - Owned by developers 
    b. Backend Testing - API testing(All validations), DB, Auth and PII data specific uses cases, basic performance to see query efficiency. Automate API's.
    c. Intergation/Component Testing - UI + Component level User flow, Expected API calling, Events, DB, Kafka, Third Party integrations, browser and device coverage. Automate UI.
    d. E2E - All user journies, communications, Event Flow, Feature Flags/configs. Automate critical flows.
    e. Resiliance testing - To check how system behaves in case of service failure and other scenarios.
    e. Performance and Security - will also include cloudfront rules(rate limiting, geo fencing...etc.), api gateways rules


3. What I will deliberately leave unautomated:

    a. Visual design aspects.
    b. Chatbot quality. LLM output is non-deterministic, so I’d use a small evaluation set with sampled human review.
    c. Browser and device coverage.
    d. Resiliance cases.
    
4. QA ownership in a pod model across 20 services

    I will organize pods around business flows, not individual services.

    Pod 1 : Pre Order including automation
    Pod 2 : Post Order including automation
    Pod 3 : Platform - Performance, Security

5. Where quality gates live in CI/CD
    
    a. Pull request : Run API suite(Module specific), Unit Test cases and coverage, Security scan. 
    b. Merge to Feature QA branch(QA Env.) : UI Sanity suite and API Regression suite. To check if feature and env. is stable enough to proceed with testing.
    Nightly-Full regression. 
    Once all major bugs are fixed - performance baseline and the Kafka soak test.
    c. Production-Release branch - UI Sanity and API regression suite(Majorly get requests)


6. QA Metrics to be tracked

    a. During Feature testing
        P0 bugs, Build rejection, Invalid/duplicate bugs, Reopen bugs, P0 cases added during review
        API and UI automation coverage
        Planned QA efforts
        Change requests
        Test case coverage as per Test Plan(some time device coverage, resiliance cases are missed)
        Automation and manual Review TTL
        Script maintenance
        Variation in feature testing compared to given estimations
        AI and automation utilization and productivity
    b. During Release
        Bug found during regression vs feature testing
        Automation Pass % and Execution time
        Bugs found via Automation
        Overall Release time    
        AI and automation utilization and productivity
        Flaky test cases
    c. Post release
        Checklist uodate
        Regression suite updated
        Updated automation execution time and coverage
        Defect Leakage
        Incident for Major bugs
        Rollback
        Revenue loss
        Logs and Infra health verified
    d. Monthly review   
        Subset from above
        DEV-QA effort Ratio
        Planned Features delivered in a quarter 
        Subject matter expert 
        Innovation
        Discipline adhering to processes

