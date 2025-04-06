FROM python:3.11-alpine
WORKDIR /usr/local/app
COPY . .
RUN pip install --upgrade pip
RUN pip install -r ./src/recommendation/requirements.txt
CMD ["python3", "recommendation_server.py"]
