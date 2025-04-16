# AWS-Based-Load-Balancing-Framework

## A Scalable Distributed System for Photo-to-Video Conversion

![Architecture Diagram](https://github.com/sskhandle/AWS-Based-Load-Balancing-Framework/blob/master/animato-master/architecture.JPG)

## Overview

This project implements a fully scalable and distributed system that converts collections of photos into video slideshows through a web-based interface. LoBUCS (Load Balancing Utility for Cloud Services) powers the dynamic scaling capability, ensuring optimal resource utilization and efficient processing of conversion tasks.

## Architecture

The system uses a serverless microservices architecture on AWS with the following components:

- **Web Interface**: Flask-based frontend for uploading photos and music
- **Task Queue**: SQS-based job distribution system
- **Processing Workers**: Auto-scaling EC2 instances that perform conversions
- **Storage Layer**: S3 buckets for media assets and final videos
- **State Management**: DynamoDB for task deduplication and tracking

## Key Features

- **Dynamic Scaling**: Automatically scales worker nodes up and down based on SQS queue depth
- **Fault Tolerance**: Built-in message deduplication and error handling
- **High Availability**: Distributed architecture with no single point of failure
- **Resource Efficiency**: Workers are provisioned only when needed and terminated when idle
- **Web-Based Interface**: Simple upload mechanism for photos and customization options

## Scaling Mechanism

The system monitors SQS queue size to make intelligent scaling decisions:

### Upscaling
When workload increases, new worker instances are automatically provisioned:

![Upscaling Process](https://github.com/sskhandle/AWS-Based-Load-Balancing-Framework/blob/master/Working1(scaling).png)

### Downscaling
When workload decreases, excess worker instances are terminated to save resources:

![Downscaling Process](https://github.com/sskhandle/AWS-Based-Load-Balancing-Framework/blob/master/Working2(scaling).png)

## Project Structure

- **`config/`**: Configuration files for AWS services and application settings
- **`setup/`**: Contains `do_setup.ipynb` for deploying Animato on EC2
- **`watcher/`**: Scaling controller that monitors SQS and manages worker instances
- **`webserver/`**: Flask application code for the web interface
- **`worker/`**: Processing logic for converting photos to videos

## Implementation

The system uses parallel processing to efficiently distribute work across multiple workers. Each worker:
1. Pulls tasks from the SQS queue
2. Downloads source assets from S3
3. Processes the photo-to-video conversion
4. Uploads the result back to S3
5. Marks the task as complete in DynamoDB

This architecture allows for processing large volumes of conversion requests with optimal resource utilization and high throughput.

## Getting Started

1. Configure your AWS credentials in the `config/` directory
2. Run `do_setup.ipynb` to provision the necessary AWS resources
3. Deploy the webserver and initial worker instance
4. The watcher service will automatically manage scaling based on demand
