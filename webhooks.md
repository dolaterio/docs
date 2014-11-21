# Webhooks

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
