# Fast API Lambda

Based on https://adem.sh/blog/tutorial-fastapi-aws-lambda-serverless

## Quickstart local

- Locally deploy with `uvicorn main:app --reload`
- Auto-generated docs at: http://127.0.0.1:8000/docs

## Quickstart lambda

- Set up credentials for serverless (with AWS profile or other means)
- Create a `.env` file with populated values (add a certificate ARN for the desired domain)
    - For AWS, create your certificate with Certificate Manager in the appropriate region and copy the ARN.
- Deploy with `sls deploy --stage v0`, where `v0` could be anything like `staging` or `live`, whatever convention suits.

**Serverless gotcha with Windows WSL2 Debian:** Had to make a manual change to a line of code in `node_modules/serverless-python-requirements/lib/docker.js`, [see here](https://github.com/serverless/serverless-python-requirements/issues/371)

- API available at `https://XXXXXXXXX.execute-api.eu-west-1.amazonaws.com/v0/` (where the first characters are returned after deploy)
- Access docs at `https://XXXXXXXXX.execute-api.eu-west-1.amazonaws.com/v0/docs` and other endpoints by replacing `docs` with your endpoint names.
