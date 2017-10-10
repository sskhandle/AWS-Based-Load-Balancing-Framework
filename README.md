# AWS-Based-Load-Balancing-Framework

## Fully scalable Distributed Load Balancing Framework to make videos out of photos

>In this project we have developed an application to convert photos to video.
>we have used flask framework to create our webserver. ec2 instances to launch web-server
>and worker. size of SQS queue to scale up and down the workers. dynamoDB to avoid duplicate
>message from sqs. S3 to store photos

## Architecture

![drawing](https://github.com/sskhandle/AWS-Based-Load-Balancing-Framework/blob/master/animato-master/architecture.JPG)

### Files

* config	give your configration here
* setup  	run do_setup.ipynb to setup Animato on ec2
* watcher	to scale workers up and down depending SQS system
* webserver	contains webserver code
* worker        contains worker code
