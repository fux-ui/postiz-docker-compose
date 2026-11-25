## Deploy on Coolify

1. Add an application from the public repository `https://github.com/fux-ui/postiz-docker-compose` using branch `coolify`, the Docker Compose build pack, base directory `/` and Compose location `/docker-compose.yaml`. Use Coolify's managed Compose deployment.
2. Enable **Preserve repository during deployment** so Temporal can read `dynamicconfig/development-sql.yaml` from the read-only repository mount. For an existing installation, check that the six volume mappings point to the existing data before deploying.
3. Reload Compose so Coolify generates and stores three independent random hex values using its `SERVICE_HEX_64_*` environment variables. For existing data, reuse the established JWT and database credentials. PostgreSQL initialization variables do not rotate existing passwords. Use a URL-safe database password or percent-encode it in the Postiz database URL.
4. Route HTTPS for `post.fuxu2.tech` to the `postiz` service on internal port `5000`. In Coolify versions with a single per-service domain field, enter `https://post.fuxu2.tech:5000`. Point DNS at the Coolify proxy and enable the HTTP-to-HTTPS redirect. The public URL is `https://post.fuxu2.tech`.
5. Deploy, check the Postiz and Temporal health status in Coolify, and open the public URL to verify TLS and the Postiz login page.

Optional integration credentials can be entered in Coolify by their corresponding environment variable names in the Compose file.


## Watch the Tutorial for docker-compose install:
[https://m.youtube.com/watch?v=A6CjAmJOWvA&t=5s](https://m.youtube.com/watch?v=A6CjAmJOWvA&t=5s)

## Warning
If you are upgrading from Postiz old version, please make sure you update your docker compose, you can read more here:
https://docs.postiz.com/installation/migration

### Configuration uses environment variables

The docker containers for Postiz are entirely configured with environment variables.

- **Option A** - environment variables in your `docker-compose.yml` file
- **Option B** - environment variables in a `postiz.env` file mounted in `/config` for the Postiz container only
- **Option C** - environment variables in a `.env` file next to your `docker-compose.yml` file (not recommended).

... or a mixture of the above options!

There is a [configuration reference](https://docs.postiz.com/configuration/reference) page with a list
of configuration settings.

Setup:
```
git clone https://github.com/gitroomhq/postiz-docker-compose
```

Then run:
```
docker compose up
```

Wait for it to load:

Open your website on https://localhost:4007
