Solution architecture
==

Specific architecture decisions will be documented in their corresponding
repositories. With that said, we will generally use the following technologies:

* **Express** for server-side API and models
* **Vue** for front-end and client-facing UX
* **SASS** for structured styling and responsive CSS
* **Webpack** for bundling of client-side Javascript

Whenever appropriate, new applications which can be built off the main services
API will be structured as independent lightweight front-end applications.

Following best practices, all applications store sensitive configuration in the
environment and not the codebase. Local configuration can generally be specified
in `config/local.js` which is excluded from GIT.

#### Logging and metrics

[Winston](http://GitHub.com/winstonjs/winston) is used to declare various levels
of verbosity in the log output. In production, only `info` level and above will
be sent to [Logentries](https://logentries.com) for storage and aggregation.
In development, the logging output can be adjusted for individual debugging
needs but defaults to `verbose` and above.

In addition to standard logging, exception tracking in Production on both the
server and the client will be reported through
[Raygun](https://raygun.io/products/crash-reporting). This will include
aggregation of full stack traces along with details on the user and browser
when the exception occurred.

[OpBeat](https://opbeat.com) is used for storage and aggregation of performance
metrics from applications running in production. In addition, it will serve as
uptime monitor and emergency alerts in the case of an issue in production.

#### Deployment

[Heroku](https://www.heroku.com) is used for all production applications, QA
environments, and review apps. Each application will be configured in a [Pipeline](https://devcenter.heroku.com/articles/pipelines). This ensures that
all code being reviewed at any stage in the feature development lifecycle is
done so on an exact replica of the production environment.

[IBM Compose](https://www.compose.io) is used for all databases and provides
automated backups and disaster recovery in addition to general database
environment optimization and configuration.

Due to ephemeral file systems on all production applications, any permanent file
storage will utilize [Amazon S3 buckets](https://aws.amazon.com/s3/). When files
are uploaded by users, a CORS upload will be used to transfer the file directly
between the user and S3 without involving the production application.

[Cloudflare](https://www.cloudflare.com) is used as both a CDN and a layer of
threat mitigation. If custom proxying is required an additional proxy server may
be used which runs [NGINX](http://nginx.org). Generally, all caching should be
deferred to either Cloudflare **_or_** NGINX to avoid cache conflicts and
prevent deployment complications.
