# Temperature sensor with led warning project
## Author: Strilciuc Gabriel

## Description
This application runs on a Raspberry Pi Zero W and a breadboard. The sensor data is displayed on a website powered by Django and Celery.

This project can be ported to other Raspberry Pi machines with more hardware resources if needed. 

The Django framework helps creating a quick web server and Celery is a Distributed Task Queue as the developer himself calls it, which helps the server-side tasks to be asynchronous and boost its response time.

## Getting Started

### Installing

This project uses django and celery, therefore the raspberry pi machine should have those installed. I recommend running them on python3. 

First, you need to make sure the machine is updated, for this run in a terminal those commands:
```
    $ sudo apt-get update
    $ sudo apt-get upgrade
```

Check if you have python3 installed by running in command line:
```
    $ python3
    >>>quit()
```

The first command should run the python3 interpretor, if it exists, then the quit() method exits it.

If not found, installing the python3 interpretor is not hard:
```
    $ sudo apt-get install python3
```

With those installed, proceed to install django and celery:
```
    $ sudo pip3 install django
    $ sudo pip3 install celery
```

I recommend installing those with sudo privileges, because we need sudo for running the website on HTTP port 80. Also rebooting the machine can be an option here, but not needed.

The celery framework needs a message broker: redis or rabbitMQ are one of those.

Installing redis:
```
    $ sudo apt-get install redis
    $ sudo pip3 install redis
```

### Running the application

After all those required packages installed, we need to run a celery worker. Enter the app folder and execute:
```
    $ sudo celery -A temp_website -l info -n worker
```
If you consider usefull runing more than one worker on the machine, it is possible. Just run the previous command with a different name in the "-n" argument. The workers will automatically syncronize.

Run the django project from the app folder with:
```
    $ sudo python3 manage.py runserver ip:80
```

The ip bit in the command should be the local ip of the machine you are running this app on. If it is hard to find out your local network ip run those commands:
```
    $ python3
    >>>import socket
    >>>socket.gethostbyname_ex(socket.gethostname())[-1][-1]
```

## Acknowledged problems

Using this build is resource demanding, it may be not optimal to be run on a Raspberry Pi Zero W as the response times can be high.

Also using the multiprocessing tool on a single threaded computer doesn't bring the best result.

## Resources and references

[Django documentation](https://towardsdatascience.com/image-panorama-stitching-with-opencv-2402bde6b46c)

[Celery documentation](https://docs.celeryproject.org/en/stable/)