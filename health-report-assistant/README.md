## Set up and launch application

## Pre-requisites

1. It is assumed that Python3+ is installed or download from <https://www.python.org/downloads/>.
2. It is assumed that Node.Js is installed or download from <https://nodejs.org/en/download>.
3. watsonx Assistant on IBM cloud.
   **Steps to create watsonx Assistant**

- 3.1 In the IBM cloud console, go to **Catalog > watsonx Assistant**
- 3.2 Fill up the necessary details and click **Create** to create an instance.
- 3.3 Once instance is created, go to the insatance & click **Launch watsonx Assistant**
- 3.4 Follow steps **Create New > provide Assistant name > Create assistant**
- 3.5 In the `frontend` directory, we have provided `healthcare-qna-WA.zip` file which will be used in next step.
- 3.6 From left hand side panel, go to **Assistant settings > Download/Upload files > Upload > upload the social-media-intelligence-WA.zip > Upload and replace**
- 3.7 Once upload is complete, the watsonx Assistant is ready & you can find all the actions under left hand side panel **Actions > Create by you**
- 3.8 Customize your chat UI. Go to left hand side panel **Environments > Draft > Web chat > Style** and change the Assistant's name as 'Healthcare'. Click Save and exit button.
- 3.9 Edit the default Home screen. Go to left hand side panel **Environments > Draft > Web chat > Home screen** and disable home screen.
- 4.0 Note down the assistant keys `integrationID`, `region` & `serviceInstanceID`, which will be used in setting the Environment file in next section. Go to left hand side panel **Environments > Draft > Web chat > Embed**

4. A watsonx.ai instance on IBM cloud ([get a watsonx trial account](https://dataplatform.cloud.ibm.com/registration/stepone?context=wx)).

### Run the backend server

1. Go to the `server` directory and prepare your python environment.

   ```sh
   python3 -m venv client-env
   ```

2. Activate the virtual environment:

   - MacOS, Linux, and WSL using bash/zsh

   ```sh
   source client-env/bin/activate
   ```

   - Windows with CMD shell

   ```cmd
   C:> client-env\Scripts\activate.bat
   ```

   - Windows with git bash

   ```sh
   source client-env/Scripts/activate
   ```

   - Windows with PowerShell

   ```cmd
   PS C:> client-env\Scripts\Activate.ps1
   ```

   > if there is an execution policy error, this can be changed with the following command

   ```cmd
   PS C:> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

3. Install the required libraries.

   ```sh
   pip3 install -r requirements.txt
   ```

4. [Get a watsonx trial account](https://dataplatform.cloud.ibm.com/registration/stepone?context=wx).

5. Add `.env` file to your application folder and add env variable

   ##### Steps to create IBM Cloud API key

   - 5.1.1 In the [IBM Cloud console](https://cloud.ibm.com/), go to **Manage > Access (IAM) > API keys**
   - 5.1.2 Click **Create an IBM Cloud API key**
   - 5.1.3 Enter a name and description for your API key
   - 5.1.4 Click **Create**
   - 5.1.5 Then, click **Show** to display the API key. Or, click **Copy** to copy and save it for later, or click **Download**

   ##### Steps to create project_id (skip 5.2.1 to 5.2.3 for watsonx trial account)

   - 5.2.1 In IBM Cloud, [Set up IBM Cloud Object Storage for use with IBM watsonx](https://dataplatform.cloud.ibm.com/docs/content/wsj/console/wdp_admin_cos.html?context=wx&audience=wdp)
   - 5.2.2 [Set up the Watson Studio and Watson Machine Learning services](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/set-up-ws.html?context=wx&audience=wdp)
   - 5.2.3 Create a Project from IBM watsonx console - https://dataplatform.cloud.ibm.com/projects/?context=wx
   - 5.2.4 (Optional step: add more collaborators) Open the Project > Click on **Manage** tab > Click on **Access Control** from the **Manage** tab > Click [Add collaborators](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/collaborate.html?context=wx&audience=wdp#add-collaborators) > **Add Users** > Choose **role** as **Admin** > Click **Add**
   - 5.2.5 Click on **Manage** tab > Copy the **Project ID** from **General**

     ```sh
     GENAI_API = https://us-south.ml.cloud.ibm.com
     GENAI_KEY=<your IBM Cloud API key>
     PROJECT_ID=<your watsonx.ai project_id>
     ```

6. Run the application.

   ```sh
   python3 app.py
   ```

Now your backend server is up and running at the following URL.

```url
http://localhost:5000
```

### Run the frontend app

1. Go to the `frontend` directory.

2. Install the required packages.

   ```sh
   npm install
   ```

3. Add `.env` file to your application folder and add env variable

```sh
 # as our backend server is running at the below URL
 REACT_APP_BACKEND_URL = http://localhost:5000
 REACT_APP_WA_INT_ID = <watsonx assistant integration id>
 REACT_APP_SVC_INST_ID = <watsonx assistant instance id>
 WX_PROJECT_ID = <your watsonx.ai project_id>
 WX_ENDPOINT = https://us-south.ml.cloud.ibm.com
```

4. Run the frontend app
   ```sh
   npm run start
   ```

You can now access the application from your browser at the following URL.

```url
http://localhost:80
```
