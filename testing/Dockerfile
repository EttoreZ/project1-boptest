FROM michaelwetter/ubuntu-1604_jmodelica_trunk

USER root

RUN apt-get update && \
    apt-get install -y git && \
    apt-get install -y sudo

USER developer

ENV ROOT_DIR /usr/local

WORKDIR $HOME

RUN git clone https://github.com/ibpsa/modelica-ibpsa.git $HOME/git/ibpsa/modelica-ibpsa && \
    git clone https://github.com/lbl-srg/modelica-buildings.git $HOME/git/buildings/modelica-buildings && \
    cd $HOME/git/ibpsa/modelica-ibpsa && git checkout ed4df71 && \
    cd $HOME/git/buildings/modelica-buildings && git checkout 1a6d3a768cf43f43b4e434997653734f85f722d8

RUN python -m pip install --user pandas==0.22.0 requests

WORKDIR $ROOT_DIR

ENV JMODELICA_HOME $ROOT_DIR/JModelica
ENV IPOPT_HOME $ROOT_DIR/Ipopt-3.12.4
ENV SUNDIALS_HOME $JMODELICA_HOME/ThirdParty/Sundials
ENV SEPARATE_PROCESS_JVM /usr/lib/jvm/java-8-openjdk-amd64/
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
ENV PYTHONPATH $PYTHONPATH:$JMODELICA_HOME/Python:$JMODELICA_HOME/Python/pymodelica:/usr/local/testing
ENV MODELICAPATH $MODELICAPATH:$HOME/git/buildings/modelica-buildings:$HOME/git/ibpsa/modelica-ibpsa