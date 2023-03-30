# Deployment

## 1. Creating an account: 
In order to use the API from anywhere on any machine, one would need to deploy the API to a hosting service. The hosting service we picked is [render](https://render.com). 

(if an account has not already been created) When signing up for an account, make sure to do so using the GitHub account which owns the repository containing the code you'd like to deploy. This is to make it convenient for quickly selecting repositories on your GitHub account direcly from within [render](https://render.com).

## 2. Creating a new service: 

1. After logging in, click the 'new +' button near the profile icon and select webservice. Selecting webservice allows us to deploy applications that will be serving data to its users. Please check out the [Web Services documentation](https://render.com/docs/web-services) on render.

![image](https://user-images.githubusercontent.com/97417536/227998672-545b6d4c-d7a5-4f14-b137-43d182c32331.png)

2. Select the GitHub repository containing the code you'd like to deploy. In this case, it will be ``cool-corridors-API``

![image](https://user-images.githubusercontent.com/97417536/228000965-951b5bcb-3af5-420a-a80e-abf0fc992b9d.png)

3. You will now be greeted with this menu to fill out:

  ![image](https://user-images.githubusercontent.com/97417536/228002777-a42f487c-812e-4986-a030-c91679dfcb48.png)
  
Here's what each field mean, feel free to also checkout the [documentation](https://render.com/docs/web-services#deploy-your-own-code):
  
  - ``Name``: A name for your Web Service
  - ``Runtime``: The programming language of your code, which is Python. 
  - ``Region``: The [geographic region](https://render.com/docs/regions) to deploy to
  - ``Branch``: The git branch to build. At the moment, the branch used is ``gunicorn-testing``
  - ``Root directory``: The directory which the application is ran from. Keep this as default because the root directory contains a file named ``run.py`` which is responsble for running the code in ``/src``
  - ``Build Command``: The command to build your Web Service. Because all the API dependencies of the project are in `requirements.txt`, set this field to ``pip install -r requirements.txt``. If new packages/dependencies are later on added to the project, run ``pip freeze > requirements.txt`` within the project root directory to get an up to date ``requirements.txt`` file.  
  - ``Start Command``: The command to start your Web Service. The command is ``gunicorn run:app`` where ``app.py`` is in the root directory of the repository. We decided to use [gunicorn](https://gunicorn.org/) because it can make the application handle more requests per second. More on this is elaborated below. 

### Why use gunicorn? 
  
Flask is a light weight framework great for developing applications locally on your machine. However, flask on its own can only handle one request at a time in sequential order, making it less ideal for deployment into production. 

Turns out that its best practice to run flask code using [gunicorn](https://gunicorn.org/). 
This is because gunicorn uses a [pre-fork model](https://docs.gunicorn.org/en/stable/design.html) which has 
multiple processes called "workers" that can indidivually handle API requests. These processes are handled by a "Master Process" that manages the number of running workers based on how many API requests are made at a given time. 
The result is that we have a faster application that can handle multiple requests at the same time as opposed to just one at a time. 

[article](https://blog.ironboundsoftware.com/2016/06/27/faster-flask-need-gunicorn/)

  ## Plan
  Scrolling further down from ``Start Command``, you can select the plan to host the API with. You can specify the amount of RAM and how many CPUs your Web Service requires. We selected the free plan for now, but higher tiers can handle more traffic load.
  
  ![image](https://user-images.githubusercontent.com/97417536/228021569-ada52763-f00f-4b4f-a22c-e9549d925dae.png)

  ## Advanced: 
  
  Within ``Advanced``, you may also specify environment variables, secrets, persistent disk, health check path, and whether or not to auto deploy on every git push.
  
  ![image](https://user-images.githubusercontent.com/97417536/228029117-93da1d34-41e4-4569-9381-fea5f443030a.png)

  For this section, we need to do two things:
  
  1. Add an environment variable to specifiy the Python version for render to use for deployment. 
  
  ```
  Key: PYTHON_VERSION
  Value: 3.9.10
  ```
  
   ![image](https://user-images.githubusercontent.com/97417536/228029988-7ef15efa-2c03-4915-b5ac-45c082ccdc8f.png)
 
 2. Add a `.env` file containing PurpleAir API read and write keys. Conventionally, `.env` is added to the `.gitignore` of project repositories in order to keep senstitive information needed to run the API hidden and safe. However, there's no way for render to have access for this file unless we explicitly specify it here:
  
  ![image](https://user-images.githubusercontent.com/97417536/228032291-aa7e0043-bc7d-49a2-8ece-4b59b76d33bb.png)
  
  - Filename: ``.env``
  - contents: 
   
     ```ini
     Make sure to have the keys enclosed in quotiation marks
     
     READ_KEY = "INSERT_READ_KEY_HERE"
     WRITE_KEY = "INSERT_WRITE_KEY_HERE"
     ```

**Once all of this has been set, click the Create Web Service button all the way at the bottom:**

![image](https://user-images.githubusercontent.com/97417536/228036086-da582277-8da2-4405-983d-41f64e7298f6.png)

