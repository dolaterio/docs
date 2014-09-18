# Jobs

A job in dolater.io represents a process. When our servers run a job, takes the docker image and runs it.

Jobs can have STDIN. This is sent to the docker container and most probably sent to the process that your image runs.

Jobs can also have job-specific environment variables. When a job runs, it receives the environment variables from the image and from the job, merging them. If the job and the image specifies the same variables, the job value is used.


