FROM jupyter/base-notebook
USER root
RUN apt -y update &&  apt -y install libpq-dev gcc \
    && pip install psycopg2

USER jovyan
COPY ./task1.ipynb ./task1.ipynb
CMD ["jupyter", "lab", "--no-browser","--NotebookApp.token=''","--NotebookApp.password=''"]
