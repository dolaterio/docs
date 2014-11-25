# Webhooks

# Outgoing webhooks

Any image can have multiple outgoing webhooks to integrate dolater.io with your app.

In the image form (creation or edit) you can add multiple URLs as _Outgoing webhooks_

When a job in that image is marked as completed, a POST request is sent to your image with the following fields:

+ `image_id`
+ `job_id`
+ `created_at`
+ `exit_status`
+ `duration`
+ `stdout`
+ `stderr`
+ `error`

Those values are the same you can see in the job details.


## Incoming webhooks

Any image can have multiple incoming webhooks to create jobs just sending a POST request to it.

The incoming webhooks URLS are randomized and unique, so you can generate and destroy them anytime.

The jobs created from this webhooks will get to the STDIN all the body sent to the http request.
