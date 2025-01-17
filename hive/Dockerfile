FROM openjdk:8u242-jre as builder

USER root

ENV HADOOP_VERSION=3.2.0
ENV METASTORE_VERSION=3.0.0

ENV HADOOP_HOME=/opt/hadoop-${HADOOP_VERSION}
ENV HIVE_HOME=/opt/apache-hive-metastore-${METASTORE_VERSION}-bin

WORKDIR /opt


RUN curl -L https://archive.apache.org/dist/hive/hive-standalone-metastore-${METASTORE_VERSION}/hive-standalone-metastore-${METASTORE_VERSION}-bin.tar.gz | tar zxf - && \
    curl -L https://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz | tar zxf - && \
    wget --no-check-certificate  https://jdbc.postgresql.org/download/postgresql-42.2.24.jar -o ${HIVE_HOME}/lib/postgresql-42.2.24.jar

COPY ./metastore-site.xml ${HIVE_HOME}/conf
COPY ./entrypoint.sh .

RUN groupadd -r hive --gid=1000 && \
    useradd -r -g hive --uid=1000 -d ${HIVE_HOME} hive && \
    chown hive:hive -R ${HIVE_HOME} && \
    chown hive:hive entrypoint.sh && chmod +x entrypoint.sh



EXPOSE 9083

ENTRYPOINT ["sh", "-c", "./entrypoint.sh"]
