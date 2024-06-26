
# Installation

In this section, we're going to walk you through how you can install and set up everything you need to run LaVague locally.

!!! tip "Colab"
    If you just want to test out LaVague without having to install anything locally, you can run our [Quick Tour notebook with Google Colab](https://colab.research.google.com/github/lavague-ai/lavague/blob/main/docs/docs/get-started/quick-tour-notebook/quick-tour.ipynb).

To start using LaVague, we need to install a webdriver and store it in our home directory, so that LaVague can interact with the browser using underlying automation tool `Selenium`. We will then also install the LaVague package.

!!! note "Playwright integration"
    Alternatively, we support using Playwright for our `lavague build` command, which does not require webdriver installation. With the `lavague build` CLI command, you can generate Python files with automation code to carry out actions from text instructions! See our [playwright guide](./playwright.md) to see how to get started with Playwright. 

We provide two key installation options:

- Setting up LaVague in your environment [with our installation script](#local-setup)
- Running LaVague with [the Lavague docker image](#docker-setup)

## Local setup

To set-up LaVague in your local linux environment, you can run our `setup.sh` script:

`bash setup.sh`

To set-up LaVague in your local macos environment, you can run our `setup-macos.sh` script:

`bash setup-macos.sh`

This will perform all necessary steps to set-up LaVague.

> Feel free to inspect the script before running it.

## Docker setup

To use LaVague with our docker image you will first need to:

1. Pull the latest LaVague docker image:

`docker pull lavagueai/lavague:latest`

2. Use `docker run` with the LaVague command of your choice:

`docker run -v /home/$USER/LaVague/lavague-files:/home/vscode/lavague-files -e OPENAI_API_KEY=[YOUR_OPENAI_API_KEY] lavagueai/lavague:latest build`

If you end your docker run command with:

- `build`: it will execute `lavague -i instructions.yaml -c config.py build` from the root of your `lavague-files` mounted volume
- `launch`: it will execute `lavague -i instructions.yaml -c config.py launch` from the root of your `lavague-files` mounted volume
- `a custom command`: it will execute this command, for example, `lavague -i custom_instructions.yaml -config_path custom_config.py build`

⚠️ In the latter case, make sure you place the relevant files in your mounted `lavague-files` volume!

???+ info "Docker run command in more detail"

    - We need to mount the lavague-files volume with the `-v /home/$USER/LaVague/lavague-files:/home/vscode/lavague-files` option so that you can easily customize your config and instructions files and can easily acess LaVague's output files from the `build` command.

    - When using `lavague [OPTIONS] launch`, we need to ensure we bind the host system port 7860 with the container port 7860 by using the `-p 7860:7860` option. This enables us to see the Gradio generated by `lavague [OPTIONS] launch` in the container, on localhost:7860 on our local machine.

    - Any environment variables required to run our command, such as your `OPENAI_API_KEY` should be specified with the `-e` option.

## Conclusions

You are now ready to use LaVague with the integration of your choice. To see how to do this with our CLI, see our [quick tour](./quick-tour.md) or [integration pages](../integrations/api/hugging-face.ipynb).