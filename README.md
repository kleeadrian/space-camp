# Getting Started with Feature Flags by LaunchDarkly

![Toggle](https://cdn.glitch.com/d62580d1-04a7-4eb1-9a98-30c4d9a7fd50%2FThumbsUpLight.png?v=1579302847550)

The space camp project provides guidance on how to easily get started with feature flags on launchdarkly and turning on features for a specific group of users. 

Contents
---

To be filled



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
7. <img width="1364" alt="Screen Shot 2021-12-10 at 12 54 14 am" src="https://user-images.githubusercontent.com/22606299/145411020-4bc5e255-c72c-43c2-8a03-0ecd233007e3.png">

8. Open up server.py in the space-camp folder and replace 'LD_SD_KEY' on line 12 with the key you copied Example:
    + `ldclient.set_sdk_key(os.getenv('XXXX-XXXXX-XXXXX-XXXXX-XXXXX'))`
    
9. Type in the following command in terminal and navigate to http://127.0.0.1:5000 to see the following page
    + `python3 server.py`


![image](https://user-images.githubusercontent.com/22606299/145411817-79e15b42-8b4c-487b-8813-7ffd78861e63.png)




