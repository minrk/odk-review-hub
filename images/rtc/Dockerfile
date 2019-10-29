FROM registry.gitlab.com/sagemath/sage/sagemath-dev:9.0.beta3-py3

RUN sudo apt-get update && sudo apt-get -qy install graphviz build-essential git npm nodejs && sudo apt-get clean
RUN sage -i gap_packages && rm -rf /home/sage/sage/upstream
RUN sage -pip install --no-cache-dir --upgrade ipywidgets
RUN sage -pip install --no-cache-dir dot2tex
RUN sage -pip install --no-cache-dir RISE
RUN sage -pip install --no-cache-dir nbdime
RUN sage -pip install --no-cache-dir git+https://github.com/nthiery/sage-gap-semantic-interface/
RUN sage -pip install --no-cache-dir git+https://github.com/nthiery/sage-semigroups/

ENV SAGE_ROOT=/home/sage/sage
ENV PATH=$SAGE_ROOT/local/bin:$PATH

RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - \
 && sudo apt-get install -y nodejs \
 && sudo apt-get clean

ENV JUPYTERLAB_SRCDIR=/home/sage/src/jupyterlab
ENV JUPYTERLAB_REF=371ebbb4c3f15d3797b70a9721eb12faf84b0335

RUN mkdir -p $JUPYTERLAB_SRCDIR \
 && cd $JUPYTERLAB_SRCDIR \
 && git init \
 && git remote add origin https://github.com/minrk/jupyterlab \
 && git fetch --depth 1 origin \
    odk \
 && git checkout $JUPYTERLAB_REF

RUN cd $JUPYTERLAB_SRCDIR \
 && sage -pip install -v -e . \
 && jlpm install \
 && jlpm run build \
 && jupyter lab clean


RUN sage -pip install --no-cache nbgitpuller jupyterhub==1.0.*

COPY jupyter_notebook_config.py /etc/jupyter/

USER root

ENV HOME=/home/user
ENV USER=sage

RUN mkdir $HOME \
 && chown $USER $HOME \
 && usermod -d $HOME $USER
USER $USER

WORKDIR $HOME

ADD entrypoint /usr/local/bin/entrypoint
ENTRYPOINT ["/usr/local/bin/entrypoint"]
