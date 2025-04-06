FROM python:3.12-slim-bookworm
WORKDIR /usr/local/app
COPY . .
RUN pip install --upgrade pip
RUN pip install -r /usr/local/app/requirements.txt
CMD ["python3", "/usr/local/app/recommendation_server.py"]
