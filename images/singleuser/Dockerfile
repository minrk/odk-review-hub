FROM jupyter/scipy-notebook:ad3574d3c5c7

ENV JUPYTERLAB_SRCDIR=/tmp/src/jupyterlab
ENV JUPYTERLAB_REF=371ebbb4c3f15d3797b70a9721eb12faf84b0335

# RUN mkdir -p $JUPYTERLAB_SRCDIR \
#  && cd $JUPYTERLAB_SRCDIR \
#  && git init \
#  && git remote add origin https://github.com/minrk/jupyterlab \
#  && git fetch --depth 1 origin \
#     odk \
#  && git checkout $JUPYTERLAB_REF

# RUN cd $JUPYTERLAB_SRCDIR \
#  && pip install -v -e . \
#  && jlpm install \
#  && jlpm run build \
#  && jupyter lab clean

RUN conda install -yq dxchange tomopy \
 && conda clean -pity

RUN pip install --no-cache nbgitpuller jupyterhub==1.0.*

COPY jupyter_notebook_config.py /etc/jupyter/

# USER root

# ENV HOME=/home/user
# ENV USER=sage

# RUN mkdir $HOME \
#  && chown $USER $HOME \
#  && usermod -d $HOME $USER
# USER $USER

# WORKDIR $HOME

# ADD entrypoint /usr/local/bin/entrypoint
# ENTRYPOINT ["/usr/local/bin/entrypoint"]
