📊 AWS Infrastructure: Compute & Monitoring Baseline
Project: Nautilus Application Performance Guardrails
1. Executive Summary
Successfully provisioned a Linux-based compute resource in the us-east-1 region and implemented an automated performance alert system. This setup ensures that the DevOps team is proactively notified via SNS if the application encounters a significant CPU bottleneck.

2. Compute Specification
Resource,Value
Instance Name,xfusion-ec2
Instance ID,i-0944f0709c09002a8
Region,us-east-1
Instance Type,t2.micro
Platform,Ubuntu 22.04 LTS

3. Monitoring & Alerting Configuration
We have established a CloudWatch Alarm to act as a fail-safe against resource exhaustion.

Alarm Name: xfusion-alarm

Metric: CPUUtilization (Namespace: AWS/EC2)

Statistic: Average

Threshold: >= 90%

Evaluation Period: 1 consecutive period of 5 minutes (300 seconds).

4. Incident Notification Architecture
When the alarm triggers, it automatically executes a notification action targeting the pre-configured SNS topic.

Target Topic: xfusion-sns-topic

Target ARN: arn:aws:sns:us-east-1:925255846495:xfusion-sns-topic

Current State: INSUFFICIENT_DATA (Initial metric collection phase)

5. Verification Log
The following validation was performed via AWS CLI:
# Alarm Configuration Confirmation:
# Name: xfusion-alarm
# State: INSUFFICIENT_DATA
# Action: arn:aws:sns:us-east-1:925255846495:xfusion-sns-topic

