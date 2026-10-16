• Why you picked these tools
    1. I picked selenium for UI automationas per my convinience for the assignment.

    2. For project it will depend upon advanced tools available in the market like           playwright which support both UI and Backend automation along with gradle and cucumber.
    Other factor will be if there is any existing framework already in place which can serve our purpose, if yes, will utilize it if no major drawback found.

    3. Team proficiency, budget and how fast we want to go.

• How you'd structure this for a team of 4, not just this assignment
    I would organize ownership around risk and end-to-end workflows, with a primary and backup owner for each area rather than assigning one QA to each service.

    1. QA Lead: Own the review, problem solving, optmize the framework and stays hands-on and coordinates with product, developers, and operations.
    2. QA 1 : Own the UI customer journey E2E : product discovery, currency, cart, checkout, payment.
    3. QA 2 : Own API automation, contract, and cross-service workflow coverage, including shipping, email, and the asynchronous order events consumed by accounting and fraud detection. Maintain reusable test data and cleanup routines.
    4. QA 3 :  UI Automation of Back office applications for fullifilment..etc.  and help QA2. 

• Where tests run in CI, on what triggers, and how failures surface
    a. Pull request : Run API suite(Module specific), Unit Test cases and coverage scan, Security scan. 
    b. Merge Feature to QA branch(QA Env.) : UI Sanity suite and API Regression suite. To check if feature and env. is stable enough to proceed with testing.
    Nightly-Full UI regression suite. 
    Once all major bugs are fixed - will run performance baseline and the Kafka test.
    c. Production-Release branch - UI Sanity and API regression suite(Majorly get requests which doesnt mutate production data)

    Failures can be seen in reports generated with slack msgs or emails to specific DL's.

• How you handle flakiness and test data
    Analysis: We will find the reason of flakiness by analysising the reports, logs and history patterns like dynamic locator, data updates from other TC's, sync issue, improper logic handling of tedious state ...etc. 

    Solution: By addind fail safe, Retry and making Test cases independant we can reduce flakiness. For tedious cases we need to build hypothesis around them and try out mukltiple solutions. 

    Test data strategy will depend on system and product. 
    
        Scenario 1 - Where data is quite dynamic: We will create a seed test data for test cases and store in DB/json files which get refreshed periodically. A script will be written to do so with required type of data like product SKU's. 
            There will be a lock mechanism on test user's if parallel execution in place in case of limited test users.
            State will be reverted post execution so other cases can reutilize the data.
    
        Scenario 2 - Where data don't change frequetly:  Seed data once generated, backup will be taken. After every execution will try to revert the changes to keep the sanctity of data.
            In case data is corrupted we can refresh the data using backup.
            Seed data can be updated as and when required.