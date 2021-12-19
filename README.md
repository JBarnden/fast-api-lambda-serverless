# FastAPI Serverless AWS API Template

Based on https://adem.sh/blog/tutorial-fastapi-aws-lambda-serverless

## Quickstart local

- `pip install -r requirements.txt`
- Locally deploy with `uvicorn main:app --reload`
- Auto-generated docs at: http://127.0.0.1:8000/docs

## Deploy

- Run `npm install` from the root of this repository
- Set up AWS credentials for serverless (with AWS profile or [other means](https://www.serverless.com/framework/docs/providers/aws/guide/credentials))
- Create a `.env` file from `.env.example`
    - Specify the desired domain for your API as the value of the `BASE_URL` env variable e.g. `api.example.com`
    - Create your certificate with Certificate Manager in the appropriate region and copy the ARN as the `CERTIFICATE_ARN` value
- Deploy with `sls deploy --stage v0`, where `v0` could be anything like `staging` or `live`, whatever convention suits.

**Serverless gotcha with Windows WSL2 Debian:** Had to make a manual change to a line of code in `node_modules/serverless-python-requirements/lib/docker.js` to get deployments working, [see here](https://github.com/serverless/serverless-python-requirements/issues/371)

- Once deployed, your API will be available at the `BASE_URL` specified e.g. `https://api.example.com/`
- Access docs at `https://api.example.com/docs` and other endpoints by replacing `docs` with your endpoints.
