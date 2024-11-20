FROM mcr.microsoft.com/devcontainers/anaconda:1-3

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY environment.yml* .devcontainer/noop.txt /tmp/conda-tmp/
RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then umask 0002 && /opt/conda/bin/conda env update -n base -f /tmp/conda-tmp/environment.yml; fi \
    && rm -rf /tmp/conda-tmp

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y --no-install-recommends upgrade

RUN conda install -c conda-forge notebook nb_conda_kernels jupyterlab jupyter_contrib_nbextensions pip

RUN useradd -u 5005 -g vscode -d "/workspaces" -m -s /usr/bin/bash k8s
RUN if [ -f "/workspaces" ]; then chown -R 5005 /workspaces; fi
USER k8s
