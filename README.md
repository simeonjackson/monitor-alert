<h1>Monitoring and Alerting in Azure</h1>

For this project, I took my [Highly Available Web App](https://github.com/simeonjackson/highly-available-webapp) and evolved it into a managed environment where the infrastructure reports its own health and security status. I wanted to take a support task such as monitoring dashboards and create add a component of self-reporting and automation that would be similiar to a work environment.
<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Log Analytics Workspace)
- Azure Monitor & Data Collection Rules (DCR)
- Kusto Query Language (KQL)
- Azure Dashboards
- Azure Action Groups (Email Alerts)

<h2>Operating Systems Used </h2>

- Ubuntu Server

<h2>Deployment and Configuration Steps</h2>

<p>
Cloud observability is critical for identifying performance bottlenecks and security breaches. In this lab, I integrated a monitoring and automation layer into a production-style VM Scale Set (VMSS) I made in a previous project.

I deployed a Log Analytics Workspace and configured a Data Collection Rule to ingest performance metrics (specifically CPU and Memory) and Linux Syslogs from all backend instances in the VMSS.

This data will be collected and sent to Azure Monitor. To easily manage these metrics in a centralized way I created a custom Azure Dashboard.

This dashboard wil track the CPU health of the VMSS in real-time. This is useful to monitor unusual spikes in CPU which could be a result of underlying infrastructure, security, or application-level problems.

Using Kusto Query Language (KQL) I created a query that is going to monitor failed SSH login attempts. This will help to monitor potential brute-force attacks or any other anomalies on our environment.

Now that I have the metrics I want to monitor and have set up a dashboard for a single pane view, I wanted a way to create alerts should there be something that needs attention.

Making security and performance alerts in Azure Monitor is an easy way to get notified should something not be performing right. I am going to create an Alert Rule that will trigger should the CPU go above 70%.

I can set my trigger to be static or dynamic. Static will require me to choose a set percentage whereas dynamic learns the typical averages of your environment and will adjust alerts from there. For this example I will just stick to static.

My favorite part of these alert rules would be the quick actions and action groups that will take an action should your trigger be hit. In this case I configured an action to send me an email should the CPU go above 70%.

I set a name for the rule and also gave it a severity score.

Using the same steps, I created a rule that will monitor and trigger should their be more than 5 failed log-in attempts within 5 minutes.

Here is a look at the two rules.

To test, I ran the Linux stress utility to ramp up the CPU and failed a bunch of log-in tests via SSH.

Looking at the Monitor alerts page you can see 10 alerts were generated.

The alert rule as followed the quick action I set and sent emails for the alerts as well.

My goal with this lab was to simulate how proactive monitoring and simple automation can take cloud data and provide easy to follow actionable insights.

Log Analytics ingests all the data for deep analysis when needed.

Azure Monitor tracks and monitors metrics.

Dashboards provide a quick high level overview.

Alerts and quick actions give proactive notifications to take action.

Thanks for reading.

-Simeon-
</p>
