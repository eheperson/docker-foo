FROM python:3.9-slim-buster
ENV PYTHONBUFFERED 1

RUN mkdir /app
WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

CMD ["python3", "manage.py", "runserve", "0.0.0.0:8000"]