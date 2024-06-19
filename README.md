# django-todo
A simple todo app built with django, with instructions to deploy it on your local machine and AWS EC2 Instance, with a pre-written Dockerfile as well.

Credits for creating this app goes to shreys7.

![todo App](https://raw.githubusercontent.com/shreys7/django-todo/develop/staticfiles/todoApp.png)
### Setup
To get the original repository by the original creator of this Web App, run the following command inside your git enabled terminal
```bash
$ git clone https://github.com/shreys7/django-todo.git
```

To get the repository which includes the Dockerfile as well to enable seemless deployment, run the following command inside your git enabled terminal
```bash
$ git clone https://github.com/HarshMalik7/django-todo.git
```

You will need django to be installed in you computer to run this app. Head over to https://www.djangoproject.com/download/ for the download guide, or use the following command
```bash
$ pip install django
```
If you are using Ubuntu on AWS EC2 Instance, use these 2 commands:
```bash
$ sudo apt-get update
$ sudo apt install python3-django
```

Once you have downloaded django, go to the cloned repo directory and run the following command

```bash
$ python manage.py makemigrations
```

This will create all the migrations file (database migrations) required to run this App.

Now, to apply this migrations run the following command
```bash
$ python manage.py migrate
```

One last step and then our todo App will be live. We need to create an admin user to run this App. On the terminal, type the following command and provide username, password and email for the admin user
```bash
$ python manage.py createsuperuser
```

That was pretty simple, right? Now let's make the App live. We just need to start the server now and then we can start using our simple todo App. Start the server by following command

```bash
$ python manage.py runserver
```

Once the server is hosted, head over to http://127.0.0.1:8000/todos for the App.

### Note
If you have deployed this app on an EC2 instance instead of your local machine, then follow these steps:
```bash
$ python manage.py runserver 0.0.0.0/8000
```
This command exposes the deployed app on port 8000 of the EC2 instance, but to enable users to access this app, we also need to set some security settings on our EC2 instance. The steps are as follows:
- Select your EC2 instance on the Web UI and go to Security.
- Click on the link under security groups.
- Scroll down and select "Edit inbound rules" under the Inbound rules tab.
- Click on "Add rule" and enter the following details:
- Type : Custom TCP
- Port Range : 8000 (should be same as the port number defined in the command written above)
- Source type : Anywhere-IPv4

This allows the inbound traffic to our web app and allows users to access it.

Also, if you wish to only allow all incoming traffic to this Web App, make an adjustment to todoApp/setting.py file using the following command (make sure you are inside the main folder of the app in your terminal):
```bash
$ vi todoApp/settings.py
```
and insert the IP Address of the users you wish to allow in the ALLOWED USERS section. Write '*' if you wish to allow all users.


### Deployment with Docker
To deploy this app seemlessly using docker, you need to first install docker on your EC2 instance. On Ubuntu, this can be done using the following commands:
```bash
$ sudo apt install docker.io
```
This command installs docker on your Ubuntu instance.

Next, you need to build the docker image from the docker file. This can be done using the command:
```bash
$ sudo docker build . -t todo-app
```
This command creates the docker image which we will use to deploy our app.

Next, we will simply run the docker image and deploy our app :)
```bash
$ sudo docker run -p 8000:8000 todo-app
```
This command tells docker to connect its port 8000 to the port 8000 of the EC2 instance, which we have already exposed using the steps defined in the previous note and run the image to deploy the app.

Cheers and Happy Coding :)
