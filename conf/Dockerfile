
FROM python:3.9-bullseye
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
WORKDIR /code
COPY conf/requirements.txt /code/
RUN pip install -r requirements.txt
COPY files/. /code/
