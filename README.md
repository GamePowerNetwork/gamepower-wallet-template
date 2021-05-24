# GamePower Wallet Template


## Run in Docker
---
First, install [Docker](https://docs.docker.com/get-docker/) and
[Docker Compose](https://docs.docker.com/compose/install/).

Then run the following command to build the docker image.

```bash
docker build -t gamepower-wallet:0.0.1 .
```

Next you can run the image in a container using the following command

```bash
docker run -p 9944:9944 gamepower-wallet:0.0.1
```

## Interacting on Polkadot.js.org
---
You can access your local running docker container here: https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944

Once here, visit `Developer -> Extrinsics` tab. Here you can select `Bob` as your selected account, select the `gamePowerWalletIntegration` module and the `createClass` method. As shown below.

You must have at least 1 asset class and token available to perform this test.
<img alt="step1" src="/images/step1.png">
