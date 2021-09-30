# Monitoring and alerting
## Monitoring
Collecting, processing, aggregating and displaying real-time quantitive data about a system, such as query counts and types, processing times, and server lifetimes.

White-box - frontend

Black-box - backend

Dashboard - Summary view of core metrics (should include 4 golden metrics)

Dependency hierarchys - Basically if X, then Y

Root cause

### Why should we monitor?
We can:
 - Analyze long-term trends (how fast is the service growing? WHat is the growth?)
 - Experiment with software (how much faster is nodeapp:alpine?)
 - Alerts - Something broke, come and fix it immeadiately __(important to have a good alerting system)__
 - Retrospective analysis - (A metric spiked, what happened?)

Bad alerting systems that ping too often cause staff to ignore alerts. (Get woken in you sleep)

Dependency hierarchys - Basically if statements
("If I know the database is slow, alert for a slow database; otherwise, alert for the website being generally slow.")
("If a datacenter is drained, then don’t alert me on its latency")

__"Messages to humans must be simple to understans and represent a clear failure"__

### The Four Golden Signals
If you can only measure 4 metrics, measure these:
1. Latency  -   Time it takes to service a request - Important to distinguish between successful and failed latency
2. Traffic  -   Measure of demand on the system *(HTTP requests per second)*
3. Errors 
    1. Explicitly   -   HTTP 500s
    2. Implicitly   -   HTTP 200 with incorrect content
    3. Policy       -   Not within targets (took longer than 1s)
4. Saturation   -   How full is the service? (an upper bound)

## Alerts
A notificiation intended to be read by a human and that is pushed to a system such as a bug or ticket queue, an email alias, or a pager. Respectively, these alerts are classified as tickets, email alerts, and pages.

Some metrics are better interpreted with measured groups [gatling-graph] (In microservies, 1 system can have an outlying value and severly affect the average)

### Simplicity is key
Three rules for designing alerting systems:
- The rules that catch real incidents most often should be as simple, predictable, and reliable as possible.
- Data collection, aggregation, and alerting configuration that is rarely exercised (e.g., less than once a quarter for some SRE teams) should be up for removal.
- Signals that are collected, but not exposed in any prebaked dashboard nor used by any alert, are candidates for removal.


## Type of SLA
- Customer-based SLA > Customised and unique to the client (A client/comapany - maybe they use unique under-used features)
- Service-based SLA > Groups customers together under 1 contract
- Multi-level SLA > Divide into sub groups (Finance departement, HR)


Prioritize metrics that are easy to collect and are most relevant to your system

Five important categories
1. Service availability
2. Error rates
3. Technical quality
4. Security
5. Business results


## Error budgets
If SLO is 99.9% > error budget is 0.1%

Equates to the amount of time that our system is ALLOWED to be down for

### Balancing reliability and new features
It's important to balance the release of new features and keeping the service reliable.

If SLO is 99.9% > error budget is 0.1%

- Focus on reliability when too much of the error budget is running out

- If a a company wide network outage occured, theres nothing to fix
- If the error budget was consumed by out of scope users (load testers and penetration testers)