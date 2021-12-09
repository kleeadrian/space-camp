# Getting Started with Feature Flags by LaunchDarkly

![Toggle](https://cdn.glitch.com/d62580d1-04a7-4eb1-9a98-30c4d9a7fd50%2FThumbsUpLight.png?v=1579302847550)

The space camp project provides guidance on how to easily get started with feature flags on launchdarkly and turning on features for a specific group of users. 




### Installation
---

Pre-req: Please make sure you have at least Python 3.8 installed 

1. Clone this project back to your local dev environment by running:
    + `git clone https://github.com/adrian-testorg/space-camp.git`
2. Navigate to space-camp folder
    + `cd space-camp`
3. Install the necessary python dependencies by running
    + `pip3 install -r requirements`

Note: You can also run this within GitHub Codespaces. No need to perform step 1 or 2.

### Setup 
---
**DO NOT COMMIT YOUR CODE WITH THE SDK KEY. THIS IS MEANT FOR A LOCAL ENVIRONMENT**

Note: This section requires access to Launchdarkly. Please sign up for a trial at https://launchdarkly.com/start-trial/
1. Login to your launchdarkly account by going to app.launchdarkly.com
2. Navigate to Account Settings
<img width="233" alt="Screen Shot 2021-12-10 at 12 53 11 am" src="https://user-images.githubusercontent.com/22606299/145409347-f3bbad6a-21d0-4a26-84ae-8a28f98ed2b0.png">
3. Click on Projects > New Projects
 <img width="1660" alt="Screen Shot 2021-12-10 at 12 53 24 am" src="https://user-images.githubusercontent.com/22606299/145410159-ced56a4c-39e6-4234-a07f-cccd462b38f7.png">
4. Provide you project a unique name. 
    Note: Good practice is to name your project that serves a group of users. For e.g. Mobile Apps, Desktop Users. In this example, I'll name it space-camp
5. Click Save
6. Copy the SDK Key of the Test environment 

**DO NOT COMMIT YOUR CODE WITH THE SDK KEY. THIS IS MEANT FOR A LOCAL ENVIRONMENT**

7. <img width="1364" alt="Screen Shot 2021-12-10 at 12 54 14 am" src="https://user-images.githubusercontent.com/22606299/145411020-4bc5e255-c72c-43c2-8a03-0ecd233007e3.png">

8. Open up server.py in the space-camp folder and replace 'LD_SD_KEY' on line 12 with the key you copied Example:
    + `ldclient.set_sdk_key(os.getenv('XXXX-XXXXX-XXXXX-XXXXX-XXXXX'))`
    
9. Type in the following command in terminal and navigate to http://127.0.0.1:5000 to see the following page
    + `python3 server.py`
    
**DO NOT COMMIT YOUR CODE WITH THE SDK KEY. THIS IS MEANT FOR A LOCAL ENVIRONMENT**

![image](https://user-images.githubusercontent.com/22606299/145411817-79e15b42-8b4c-487b-8813-7ffd78861e63.png)

### Creating Feature Flags! 
---
1. Head back to app.launchdarkly.com
2. Click on Top Left yellow button to ensure that you're navigated to the correct project and environment. Make sure its the same project as the SDK key you copied earlier (incase you have multiple projects)
3. Click on Feature Flags
<img width="1661" alt="Screen Shot 2021-12-10 at 1 51 41 am" src="https://user-images.githubusercontent.com/22606299/145419398-0a201ee6-afc3-4bc5-a8df-c744c2f140c3.png">
4. Press on Create Flag
<img width="647" alt="Screen Shot 2021-12-10 at 1 51 51 am" src="https://user-images.githubusercontent.com/22606299/145419370-db645b25-b11d-4a32-bdcb-f17bdad54b3f.png">

5. Call this feature flag pricing-tier-3 (This has to match the Feature_FLAG_KEY in the codebase. Look at Line 32 in 
[server.js](https://github.com/adrian-testorg/space-camp/blob/3edcc430ead48551a0636768728cd975f622cdcd/server.py#L32)
6. Check the SDKs using Client-ID box
7. Save
8. Change the targeting to On and press on Save Changes and the website should have an extra tier
![image](https://user-images.githubusercontent.com/22606299/145420674-f88f28bf-e65a-40d2-9c89-aa4a454d664d.png)

It should look like 

![image](https://user-images.githubusercontent.com/22606299/145420745-2b46eb72-6c92-4320-a8df-c5367b48338c.png)

### Targeting Users in Feature Flags via percentage rollout! 
---
1. Navigate back to your feature flag
2. You can perform a percentage based rollout by only rolling out to a subset of users by configuring the feature flag rule
<img width="1397" alt="Screen Shot 2021-12-10 at 2 05 41 am" src="https://user-images.githubusercontent.com/22606299/145421538-7d565c01-c64b-4243-84fb-b32f914539f1.png">
Note: You may want to roll it out 10-20% of users first, then gradually increase to 100% for minimal impact

### Targeting Users in Feature Flags via attributes
---
1. Navigate to your feature flag
2. You can also target users based on a specific attribute. E.g. Target users with letters starting with A, B and it matches a regex
![image](https://user-images.githubusercontent.com/22606299/145421953-6f62b730-db1c-41e5-abc3-fdf554b7162b.png)

Note: Find a meaningful rollout. Maybe roll it out to users on MAC first, then Android. 

You can also view the insights of people who have accessed your web app by navigating to the Insights Tab  
![image](https://user-images.githubusercontent.com/22606299/145422219-ef2eb7d8-0b6b-4ea7-8460-12741c124d85.png)

## Things to consider in Production
---
- Integrate it back to your APM to monitor any errors that may show up. A list of [integrations](https://docs.launchdarkly.com/integrations/app-performance) have been created
- Define a workflow and several approvers of each feature flag toggling. 
- Determine what scenarios would require a rollback 
- Define a rollout process by targetting users with specific OS, devices or geographies.
- Keep track of all work items and stories by integrating it back to your [work management system](https://docs.launchdarkly.com/integrations/workflow)
- Use a secret store to store all secrets
- Rotate the keys often. A Guide is available [here](https://docs.launchdarkly.com/home/relay-proxy/automatic-configuration)
- As you add more and more feature flags. It may not become scalable as management of many feature flags may be tough. One idea would be to leverage the terraform provider to create feature flags via a terraform template. Have a [look](https://registry.terraform.io/providers/launchdarkly/launchdarkly/latest/docs/resources/feature_flag) 
- Archive unused flags! 
