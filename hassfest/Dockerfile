FROM ghcr.io/home-assistant/home-assistant:beta

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

COPY entrypoint.sh /entrypoint.sh
COPY requirements.txt .

RUN \
    uv pip install -r requirements.txt \
    # Install requirements from core
    && curl -LJO https://raw.githubusercontent.com/home-assistant/core/rc/requirements_test.txt \
    && uv pip install $(grep -e "^pipdeptree" -e "^tqdm" requirements_test.txt) \
    && rm requirements_test.txt \
    && curl -LJO https://raw.githubusercontent.com/home-assistant/core/rc/requirements_test_pre_commit.txt \
    && uv pip install $(grep -e "^ruff" requirements_test_pre_commit.txt) \
    && rm requirements_test_pre_commit.txt

WORKDIR "/github/workspace"
ENTRYPOINT ["/entrypoint.sh"]

LABEL "name"="hassfest"
LABEL "maintainer"="WIT DS <hello@wit-ds.io>"
LABEL "version"="1.1"

LABEL "com.github.actions.name"="hassfest"
LABEL "com.github.actions.description"="Run hassfest to validate standalone integration repositories"
LABEL "com.github.actions.icon"="terminal"
LABEL "com.github.actions.color"="gray-dark"
