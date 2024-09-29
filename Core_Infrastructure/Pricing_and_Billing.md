# Pricing and Billing

> Online pricing Calculator : `google.com/products/calculator`

## Pricing Structure

### Per-second billing (you pay what you use)

- First Major Cloud to `deliver per-second billing` for its infrastructure-as-a-service compute offering, Compute Engine.

- Example of product that uses this kind of billing :
    - Google Kubernetes Engine (our container infrastructure as a service)
    - Dataproc (equivalent of Hadoop)
    - App Engine flexible environment VMs (a platform as a service)

### Pricing of Compute Engine

- **Applied sustained-use discounts**
    - Offers automatically `applied sustained-use discounts`, which are automatic discounts that you get for `running a virtual machine instance for a significant portion of the billing month`
    - When you run an instance for more than 25% of a month, Compute Engine automatically gives you a discount for every incremental minute you use for that instance

## How can I make sure I don’t accidentally run up a big Google Cloud bill?

- **Define budgets** at the billing account level or at the project level.
    1. A budget can be a `fixed limit`, or it can be tied to another metric; for example, a percentage of the previous month’s spend.
    2. You can also create an `Alert` when costs approach your budget limit
    3. `Reports` is a visual tool in the Google Cloud Console that allows you to monitor expenditure based on a project or services.
    4. `Quotas` :
        - Designed to prevent the over-consumption of resources because of an error or a malicious attack, protecting both account owners and the Google Cloud community as a whole.
        - `2 type of quotas` : rate quotas and allocation quotas.
            - Both applied at the project level
            - Rate quotas reset after a specific time.
        - Although projects all start with the same quotas, you can change some of them by requesting an increase from Google Cloud Support.
