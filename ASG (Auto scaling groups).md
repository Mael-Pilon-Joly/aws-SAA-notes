# Scaling Plans
Scaling plans in AWS Auto Scaling allow you to define how your resources should scale based on various factors. These plans combine dynamic scaling and predictive scaling methods to optimize resource utilization according to your specified strategy.

# Scaling Strategy
Definition: A scaling strategy determines how AWS Auto Scaling should adjust resource capacity to optimize for different goals.

Types: You can choose to optimize for:
Availability: Ensuring your application remains highly available by scaling up resources in response to increased demand.
Cost: Reducing costs by scaling down resources when demand is lower.
Balance: A mix of both availability and cost optimization.
Custom: Create a custom strategy based on your specific metrics and thresholds.

Dynamic Scaling
Definition: Dynamic scaling adjusts resource capacity in real-time based on live changes in resource utilization.
Mechanism:
Uses target tracking scaling policies.
Maintains resource utilization at a target value (e.g., keeping CPU utilization at 75%).
Similar to a thermostat maintaining home temperature by adjusting heating or cooling.

Predictive Scaling
Definition: Predictive scaling uses machine learning to forecast future resource needs based on historical workload data.
Mechanism:
Analyzes up to 14 days of historical data to forecast future demand for the next two days.
Generates scheduled scaling actions to preemptively adjust capacity based on the forecast.
Helps ensure that sufficient capacity is available before a predicted traffic spike occurs.
Aims to keep resource utilization close to the target value even before the demand hits.
Key Concepts for Predictive Scaling
Load Forecasting:

Analyzes historical data (up to 14 days) to predict future demand.
Provides forecasts in one-hour intervals and updates daily.
Scheduled Scaling Actions:

Proactively scales resources based on forecasted demand.
Adjusts minimum and maximum capacity according to scheduled actions to meet predicted loads.
Maximum Capacity Behavior:

Controls whether capacity can exceed predefined limits if the forecasted demand exceeds maximum capacity.
Ensures that you can handle unexpected demand while still following defined limits.
Comparison with SQS and SNS
Dynamic Scaling: Adjusts resources in real-time based on current demand, similar to how SQS handles messages with on-demand scaling.
Predictive Scaling: Prepares resources for anticipated load changes, akin to how SNS can notify of upcoming events but in a broader, predictive context.