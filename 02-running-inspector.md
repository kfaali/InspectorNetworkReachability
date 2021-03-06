Module 2 - Running the Inspector Report
=======================================

1.  Refresh the CloudFormation interface until the Status shows “Create Complete”

![](./images/mod2-1-create-complete.png)

2.  Click on the Stack Name

3.  Go to the Outputs tab of the Stack

![](./images/mod2-2-cloudformation-outputs.png)

4.  Make note of the DNS names. You can use these to validate the Web servers that should be publically accessible are.

    1.  The LoadBalancerFullDNS and PoCWebServer1PublicDNS should work.

    2.  PoCWebServer2PublicDNS should time out.

5.  Make note of the instance ID’s. These will help you when you review the Inspector report.

6.  Go to the EC2 console to validate the instances are running.

![](./images/mod2-3-ec2-validate.png)

Now we create the Amazon Inspector Targets and Templates. We do this manually to get a feel for how it works, but this can be automated. First, we must create the Assessment Target to include all instances, even those without the agent.

7.  Go to the Amazon Inspector service.

![](./images/mod2-4-inspector.png)

**{Note: If you have not used Inspector in this region before, you will get a different set of screens. Start by clicking a.) “Getting Started” on the Amazon Inspector page, and then b.) “Advanced Setup” on the bottom right to get to the Assessment Target screen – Step 10}**

8.  Click on Assessment Targets.

![](./images/mod2-5-targets.png)

9.  Click “Create”

10.  Fill out the screen as follows:

    1.  Name: {Whatever name you will remember}

    2.  All Instances: Uncheck the box

    3.  Use Tags

        1.  Key: NetworkReachabilityDemo

        2.  Value: True

    4.  Install Agents: Uncheck the box

![](./images/mod2-6-targets-2.png)

11.	Click “Save”

**{Note: If you have not used Inspector in this region before you should click "Next" to get to the Assessment Template screen – Step 14}**

12.	Click on Assessment Templates

13.	Click on “Create”
	
![](./images/mod2-7-templates.png)

14.	Fill out the screen as follows:

    1.  Name: {Whatever name you will remember}

    2.  Target Name: {The Assessment Target you just created} - This is only required if you have already used Inspector in this region before. Otherwise this is enabled by default.

    3.  Rules packages: Select ONLY “Network Reachability-1.1”

    4.  Duration: “15 minutes”

    5.  Assessment Schedule: Uncheck the box

15.	Click “Create” or “Create and run”

16.	Click on Assessment Runs and then the refresh icon

![](./images/mod2-8-runs.png)

17.	The status should say “Analyzing” or “Collecting data”

Now we want to publish the report to an SNS topic so we can take action. An SNS topic has been created for you in the CloudFormation Template.

18.	Click on Assessment templates

19.	Click on the right arrow next to the Assessment your created to expand the options.

20.	Click on box under "SNS topics"

21.	Click the drop down and select the Topic named {Accountnumber}:InspectorAutomation

22.	Deselect all of the events EXCEPT "Findings Reported".

23.	Click Save

At this point the Inspector Assessment can take up to 15 minutes. So now’s a good time to go over the architecture. The [Presentation](./resources/demo-support-presentation.pdf) includes the architecture diagram, the route tables, and the security groups. The [Presentation Notes](presentation-notes.md) page then walks through the architecture with some probing questions.

You can also choose to skip to [Evaluating Findings](03-evaluate-findings.md) once the report is complete.