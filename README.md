# FastAPI Serverless AWS API Template

Based on https://adem.sh/blog/tutorial-fastapi-aws-lambda-serverless

## Prerequisites

- Node installation (tested with `v18.7.0`)
- Python
- Docker (required for packaging dependencies)
  - You can alternatively set `dockerizePip` to `false`

## Quickstart local

- Create and activate your Python virtual environment (Python 3.9 recommended)
  - `python -m venv .venv`
  - `source .venv/bin/activate`
- `pip install -r requirements.txt`
- Run locally with `uvicorn main:app --reload`
- Auto-generated docs at: http://127.0.0.1:8000/docs

## Configure environments & Deploy

- Run `npm install` from the root of this repository
- Set up AWS credentials (AWS profile or [other means](https://www.serverless.com/framework/docs/providers/aws/guide/credentials))
- Create a `.env` file from `.env.example` for your local environment
- Create an additional env file each environment you intend to deploy (e.g. `.env.staging`)
- Specify the desired domain for your API as the value of the `BASE_URL` env variable e.g. `api.example.com`
  - Create your certificate with Certificate Manager **in the us-east-1** region
  - Copy the ARN of the certificate and use it as the value for `CERTIFICATE_ARN` in `.env`

### Deploy

- Ensure that Docker is running (or set `dockerizePip` to `false`)
- Deploy with `NODE_ENV=staging sls deploy --stage staging`, where `staging` can be substituted for any environment name.
- To deploy with specific AWS profile, use the `--aws-profile` flag, e.g. `NODE_ENV=staging sls deploy --stage staging --aws-profile default`

### Remove deployment

With credentials configured, run:

- `sls remove --stage staging`
- Manually remove the certificate you created for your domain
