FROM python:3.11-alpine
WORKDIR /usr/local/app
COPY ./src/recommendation/requirements.txt .
RUN pip install -upgrade pip
RUN pip install requirements.txt
COPY . .
CMD ["python3", "requirements.txt"]
