# Images

An image in dolater.io represents the code that the workers will run.

Images are basically docker images with some execution parameters like the environment variables.

Those environment variables are sent to ALL the jobs created on this image. Therefore it's recommended to use image environment variables for global values like authentication keys, global configuration values, etc.

