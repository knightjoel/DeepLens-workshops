In this lab session, you will learn how to build and train a model in Amazon SageMaker.

Before we begin, download the repo to your local directory. You can download the repo from [root directory](https://github.com/knightjoel/DeepLens-workshops).

Click the **Clone or download** button on the right and choose **Download ZIP**.

![github clone-edited](https://user-images.githubusercontent.com/11222214/38658212-046fee60-3dd9-11e8-9069-a71804c222b7.jpg)

This will download the repo as a zip file. Extract the zip file. 

### Step 1- Create notebook instance

NOTE: You need to build your SageMaker resources in the **US East Virginia** region in order to access the necessary S3 buckets.

Go to SageMaker console: https://console.aws.amazon.com/sagemaker

Click on **Create Notebook instance**

![sagemaker home](https://user-images.githubusercontent.com/11222214/38313489-01929ca2-37d9-11e8-9ffb-4385e8d13da3.JPG)

### Step 2- Notebook specifications

1. Provide the name of the notebook as `face-detection-`_your-name_
2. Notebook instance type: `ml.t2.medium`
3. Elastic Inference: `None`
3. IAM role: Click **Create a new role**

In the dialog box that opens up:

1. Click **Any S3 bucket**
2. Leave the rest as is 
3. Click **Create role**

![create iam role](https://user-images.githubusercontent.com/11222214/38313888-e07281e4-37d9-11e8-8b99-dd322a76ced6.JPG)


Leave VPC, Lifecycle and Encryption key as defaults. Don't make any changes.

![notebook instance setting](https://user-images.githubusercontent.com/11222214/38313994-2916257c-37da-11e8-823a-733f2572f61d.JPG)

Click **Create notebook instance**.

### Step 3- View notebook instances

You can view all your notebook instances by choosing **Notebook instances** on the left menu. It will take couple of minutes for the notebook instance to be created.

![instances](notebook_instances.png)

### Step 4- Upload and open notebook

Open the Jupyter Notebooks interface for the notebook instance you just created
by clicking on **Open Jupyter** in the Actions column.

- Extract the zip file you downloaded earlier and find the
`SSD_Object_Detection_SageMaker_v3.ipynb` file. You'll find it in the
`SageMaker lab` folder.
- In the Jupyter Notebooks interface, click the **Upload** button, browse
to the `SSD_Object_Detection_SageMaker_v3.ipynb` file and upload it.
- The file should now appear in the list of files in Jupyter Notebooks. Click
the file name which will open it in Jupyter Notebooks.

![jupyter](https://user-images.githubusercontent.com/11222214/38314946-427aa6e4-37dc-11e8-91bf-658ebe7b2a7b.JPG)

### Step 5- Execute notebook

Execute the cells by clicking on the `Run` button or using shift+enter on your keyboard.

**NOTE** the notebook will execute each cell in turn so you must click
the **Run** button once for each cell in the notebook.

![run](https://user-images.githubusercontent.com/11222214/38316244-21a07194-37df-11e8-9821-21d5d6e57976.JPG)


