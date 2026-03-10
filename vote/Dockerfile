FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt /app
RUN pip install -r requirements.txt
COPY . /app
EXPOSE 80
CMD gunicorn app:app -b 0.0.0.0:80 -w 4
