# Opportunity Priority Assignment Rules

The system will review a Salesforce Opportunity and assign a "Priority__c" score based on the following exceptions defined by the Admin. By default, the Priority__c is set to 0. The score can either be incremented or explicitly set based on the conditions provided.

The following rules will be evaluated in order. The highest priority rule that applies will be used. If no exceptions match, the Priority__c will remain 0.

### # General Instructions:
- Admin can define conditions based on Opportunity fields and their values.
- Admin can specify whether a rule should increment the priority or explicitly set it.
- Admin can cancel or supercede rules using explicit logic where necessary.

### # Priority Range:
- Priority is a 0-based integer on a scale of 0-10.

### # Exception Reporting:
Use the following format to define exceptions:

**Rule Format:**
- **Condition:** A description of when the exception should apply (based on Opportunity fields, dates, or other criteria).
- **Action:** The effect on Priority__c, whether incrementing the score or explicitly setting it to a specific value.
- **Notes:** Additional logic if this rule should cancel or override other rules.

### Examples:

1. **Condition:** If the Opportunity 'Customer_Upload__c' status is null and the StageName is 'Drafting'.
   - **Action:** Increment the priority score by 1.
   - **Notes:** This rule can be combined with others unless explicitly canceled.

2. **Condition:** If the Opportunity has been in the 'Awaiting Approval' stage for more than 3 days.
   - **Action:** Set the priority to 10.
   - **Notes:** This rule cancels out all other incremental rules and forces the Priority__c to 10.

3. **Condition:** If the Opportunity has a 'Close Date' within 7 days and StageName is 'Negotiation'.
   - **Action:** Increment the priority score by 2.

4. **Condition:** If the 'Amount' is greater than $100,000 and StageName is 'Proposal'.
   - **Action:** Set the priority to 10.

### # Overriding Logic:
- In case multiple rules apply, the highest incremented or explicit priority takes precedence unless explicitly noted otherwise.
- Conflicting rules that apply to the same condition must be resolved using override notes (e.g., "If both conditions are true, use the higher priority score").

# End of Exception Reporting