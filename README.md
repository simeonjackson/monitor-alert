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

<img width="939" height="464" alt="Image" src="https://github.com/user-attachments/assets/d8d9b832-6916-4b64-9d73-9fe2f851a6e0" />
<img width="938" height="463" alt="Image" src="https://github.com/user-attachments/assets/6bb7f595-1b36-47f6-8fcf-fdaeb7b81351" />

This data will be collected and sent to Azure Monitor. To easily manage these metrics in a centralized way I created a custom Azure Dashboard.

<img width="940" height="464" alt="Image" src="https://github.com/user-attachments/assets/de384cf5-b63a-4603-9d36-96a9537d2370" />
<img width="938" height="464" alt="Image" src="https://github.com/user-attachments/assets/a1ff7ac7-e5a9-4ffc-9a00-570bb2a82ce1" />

This dashboard wil track the CPU health of the VMSS in real-time. This is useful to monitor unusual spikes in CPU which could be a result of underlying infrastructure, security, or application-level problems.

<img width="938" height="463" alt="Image" src="https://github.com/user-attachments/assets/e9f749ae-e428-4513-bcdd-8380bc2790d1" />
<img width="931" height="461" alt="Image" src="https://github.com/user-attachments/assets/9b523470-a65f-40f8-aa80-fbe33a970d61" />

Using Kusto Query Language (KQL) I created a query that is going to monitor failed SSH login attempts. This will help to monitor potential brute-force attacks or any other anomalies on our environment.

<img width="940" height="464" alt="Image" src="https://github.com/user-attachments/assets/27dd7424-cd21-43a7-ac79-c117b75bde73" />

Now that I have the metrics I want to monitor and have set up a dashboard for a single pane view, I wanted a way to create alerts should there be something that needs attention.

Making security and performance alerts in Azure Monitor is an easy way to get notified should something not be performing right. I am going to create an Alert Rule that will trigger should the CPU go above 70%.

<img width="938" height="466" alt="Image" src="https://github.com/user-attachments/assets/831b48d2-7df7-4ecb-8032-29bea138a76d" />
<img width="931" height="461" alt="Image" src="https://github.com/user-attachments/assets/f862f7e1-c7ae-4483-9a53-97c4f59eaffb" />

I can set my trigger to be static or dynamic. Static will require me to choose a set percentage whereas dynamic learns the typical averages of your environment and will adjust alerts from there. For this example I will just stick to static.

<img width="934" height="463" alt="Image" src="https://github.com/user-attachments/assets/e3aa9414-d4cc-4b01-84ee-622e8153875f" />

My favorite part of these alert rules would be the quick actions and action groups that will take an action should your trigger be hit. In this case I configured an action to send me an email should the CPU go above 70%.

<img width="940" height="463" alt="Image" src="https://github.com/user-attachments/assets/70ce3252-1261-4a55-b408-5c8a25323058" />

I set a name for the rule and also gave it a severity score.

<img width="934" height="464" alt="Image" src="https://github.com/user-attachments/assets/da1d97ea-e8bd-470e-8132-19247b236f13" />

Using the same steps, I created a rule that will monitor and trigger should their be more than 5 failed log-in attempts within 5 minutes.

<img width="938" height="461" alt="Image" src="https://github.com/user-attachments/assets/9dc47987-2a32-4340-b668-7fa1938818bb" />

<img width="934" height="461" alt="Image" src="https://github.com/user-attachments/assets/397855f6-9420-419c-b086-04947f2cce64" />

<img width="926" height="463" alt="Image" src="https://github.com/user-attachments/assets/37212f7c-b9f8-4dce-b3bc-ebd64cb6d905" />

Here is a look at the two rules.

<img width="937" height="461" alt="Image" src="https://github.com/user-attachments/assets/7224f534-8212-4760-843f-aac52ab43961" /> 

To test, I ran the Linux stress utility to ramp up the CPU and failed a bunch of log-in tests via SSH.

<img width="868" height="465" alt="Image" src="https://github.com/user-attachments/assets/83070dc5-e326-4c0f-8358-ddf0c6ab8a32" />

Looking at the Monitor alerts page you can see 10 alerts were generated.

<img width="939" height="440" alt="Image" src="https://github.com/user-attachments/assets/7984e754-e24c-425e-96d0-1fbb299a5e6b" />

The alert rule has followed the quick action I set and sent emails for the alerts as well.

<img width="534" height="410" alt="Image" src="https://github.com/user-attachments/assets/4cfa4348-342b-48b5-8211-02f5e98a510b" />

<img width="536" height="398" alt="Image" src="https://github.com/user-attachments/assets/697b04a8-9136-475d-a832-22acb6ecdf16" />

My goal with this lab was to simulate how proactive monitoring and simple automation can take cloud data and provide easy to follow actionable insights.

Log Analytics ingests all the data for deep analysis when needed.

Azure Monitor tracks and monitors metrics.

Dashboards provide a quick high level overview.

Alerts and quick actions give proactive notifications to take action.

Thanks for reading.

-Simeon-
</p>
