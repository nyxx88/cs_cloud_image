The script "aws_cs_image3.sh" can be used to pull the following Falcon image types from CrowdStrike's image repository, so they can either be pushed into a private image repository, or be installed directly from CrowdStrike's image repository.
- Falcon Sensor for Linux (daemonset sensor) -- falcon-sensor
- Falcon Kubernetes Admission Controller (KAC) -- falcon-kac
- Falcon Image Analyzer (IAR) -- falcon-imagenanalyzer
- Falcon Container Sensor (sidecar) -- falcon-container

Basically, it uses the Falcon API client & secret to:
- Retrieve the CID value (this will be used as part of the installation commandline)
- Get the latest sensor version (this will be used to identify which image to install)

With the information retrieved:
- It will generate commandline commands for you to execute (the green colored text)
- You can just copy/paste/execute these commands to install the sensor image

<img width="1670" height="336" alt="image" src="https://github.com/user-attachments/assets/7b3c9401-5cdb-473d-b11a-fa2ff3925d3b" />

Optionally, it can create an ECR repository (assuming a valid AWS session is available). If the commandline options indicate that an ECR is to be created, then the container image specified would be copied to the newly created ECR and the generated installation commandline text will be based on ECR, and not the CrowdStrike registry. The generated commandline will have the correct image pull token for the respective registry used.

If you are deploying falcon-container sensors in AWS Fargate, the script "rm_json_tags.sh" will make things easier by removing unwanted (AWS will reject task definition files with them) tags in the 'patched' task definition file. Use this script to remove teh unwanted JSON tags before you upload the new task definition file.
