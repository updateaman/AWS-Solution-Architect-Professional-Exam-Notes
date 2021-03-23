# AWS SWF

Coordinate work amongst applications

Code runs on EC2 (not serverless)

1 year max runtime

Concept of "activity step" and "decision step"

Has built-in "human intervention" step

Example: order fulfillment from web to warehouse to delivery

Step Function is recommended to be used for new applications, except:
- if you need external signals to intervene in the process
- If you need child processes that return values to parent processes
- If you need to use Amazon Mechanical Turk