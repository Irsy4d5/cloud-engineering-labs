# Lab 04 - CloudWatch Monitoring and Alerts

Fully clean run this time, no bugs to fix - though I did hit an outdated instruction from an old console layout that's since been renamed.

## What I did

Explored CPUUtilization metrics for my lab03-test instance directly in CloudWatch, confirming AWS automatically tracks this for free without any setup. Learned that tag-based search (like searching by instance name) does not work in the metrics search box, only actual metric and dimension names do - had to filter by metric name and pick the right instance out of the list instead.

Created an alarm (lab04-high-cpu-alarm) that triggers when CPUUtilization goes above 70% for one 5-minute datapoint. Set up a new SNS topic (lab04-cpu-alerts) with my email as the notification target, then confirmed the subscription through the email AWS sent - that confirmation step is easy to miss but required, otherwise the alarm fires and nothing actually reaches you.

Finished by building a simple custom dashboard (lab04-dashboard) with a CPUUtilization line widget, the kind of thing you'd actually pull up during an incident or show in a standup.

## The interesting problem

The console UI has been updated since older guides were written - there is no "All metrics" option anymore in the sidebar, it is now called "Classic metrics." Small thing, but a good reminder that AWS reshuffles their console fairly often, so it pays to recognize what something is functionally even when the label changes.

## Commands / actions used

Fully GUI-based - CloudWatch metrics browser, alarm creation wizard, SNS topic and subscription setup, and dashboard widget creation all done through the AWS Console.

## Screenshots

lab04-dashboard.jpg: Custom dashboard showing the CPUUtilization widget

lab04-alarm.jpg: Alarm configured with the correct threshold condition

sns-subscription-confirmed.jpg: Email subscription confirmed for alerts
