FROM michaelwetter/ubuntu-1804_jmodelica_trunk

USER root

RUN apt-get update && \
    apt-get install -y git && \
    apt-get install -y sudo

USER developer

ENV ROOT_DIR /usr/local

WORKDIR $HOME

RUN mkdir $HOME/MODELICAPATH && mkdir git && \
    cd git && \
    git clone https://github.com/ibpsa/modelica-ibpsa.git && \
    git clone https://github.com/open-ideas/IDEAS.git && \
    git clone https://github.com/lbl-srg/modelica-buildings.git && \
    ln -s $HOME/git/IDEAS/IDEAS $HOME/MODELICAPATH/IDEAS && \
    ln -s $HOME/git/modelica-buildings/Buildings $HOME/MODELICAPATH/Buildings && \
    ln -s $HOME/git/modelica-ibpsa/IBPSA $HOME/MODELICAPATH/IBPSA && \
    ln -s $ROOT_DIR/JModelica/ThirdParty/MSL/Modelica $HOME/MODELICAPATH/Modelica && \
    ln -s $ROOT_DIR/JModelica/ThirdParty/MSL/ModelicaServices $HOME/MODELICAPATH/ModelicaServices
ENV MODELICAPATH $HOME/MODELICAPATH

RUN python -m pip install --user flask-restful pandas requests

WORKDIR $ROOT_DIR

ENV JMODELICA_HOME $ROOT_DIR/JModelica
ENV IPOPT_HOME $ROOT_DIR/Ipopt-3.12.4
ENV SUNDIALS_HOME $JMODELICA_HOME/ThirdParty/Sundials
ENV SEPARATE_PROCESS_JVM /usr/lib/jvm/java-8-openjdk-amd64/
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
ENV PYTHONPATH $PYTHONPATH:$JMODELICA_HOME/Python:$JMODELICA_HOME/Python/pymodelica:/usr/local/testing