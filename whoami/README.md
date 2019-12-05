# auth

Basic web application that really does nothing other than print a string to the
browser. Intended for use with an ELB demo of path-based routing.

Build the container image:

`make build`

Run the container image:

`make run`

Inspect the labels by iterating through them, and printing them each in a new line:

`make inspect`

Set the `ECR_REPO` environment variable to your ECR Repository URI. For example:

`export ECR_REPO=123456789012.dkr.ecr.us-east-1.amazonaws.com/hello`

After the build completes, tag your image so you can push the image to this repository:

`make tag`

Run the following command to push this image to your newly created AWS repository:

`make push`